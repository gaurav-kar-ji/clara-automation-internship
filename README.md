# Clara AI Automation Pipeline: Demo to Onboarding

## Architecture and Data Flow
This system is a zero-cost automation pipeline designed to transform unstructured client conversations into structured, production-ready AI voice agent configurations. The process follows a strict two-stage lifecycle to maintain data integrity and operational precision:

* **Pipeline A (Demo to v1)**: This stage ingests raw demo transcripts to extract a directional understanding of the client's needs. It generates a preliminary Retell Agent Spec and an Account Memo while strictly avoiding hallucinations by flagging missing data in a dedicated unknowns field.
* **Pipeline B (Onboarding to v2)**: This stage processes finalized onboarding audio or notes to resolve data conflicts and override preliminary assumptions with confirmed operational facts. It upgrades the agent configuration to version 2 and generates an automated changelog to track configuration drift.

## Tech Stack and Resourcefulness
To adhere to a zero-cost constraint while maintaining high engineering quality, the following tools were selected:

* **Orchestration**: Python-based modular logic for repeatable batch processing.
* **Transcription**: Local OpenAI Whisper (Base model) executed on Kaggle GPU. This allows for high-fidelity speech-to-text processing without relying on paid external APIs.
* **LLM Intelligence**: Groq API utilizing Llama 3.3 70B. This provides high-speed, structured JSON extraction at no cost for this scale.
* **Storage**: A versioned file system hierarchy that separates exploratory data from production-ready assets.

## Operational Standards and Prompt Hygiene
A core requirement of this pipeline is the generation of safe, production-ready system prompts for voice agents. The prompt generation logic follows strict hygiene rules:

* **Business Hours Flow**: Automatically configures greetings, data collection (name and number), and standard routing based on office hours.
* **After Hours Flow**: Implements a dedicated emergency screening protocol. It forces the agent to define the emergency type and immediately collect a service address for life-safety or property-damage calls.

## Project Structure
The repository is organized to demonstrate clear systems thinking and auditability:

* **workflows/**: Contains the primary automation notebook and orchestrator logic.
* **outputs/accounts/**: Organized by unique Account IDs, containing versioned subfolders (v1 and v2).
* **changelog.json**: An automated record of all modifications made during the transition from demo to onboarding.

## Setup and Execution
1. **Secrets**: Add a valid GROQ_API_KEY to your environment secrets.
2. **Input Data**: Place demo transcripts in the designated text variables and upload onboarding .m4a files to the input directory.
3. **Run**: Execute the orchestrator cells to generate the full output hierarchy and the final submission zip file.
