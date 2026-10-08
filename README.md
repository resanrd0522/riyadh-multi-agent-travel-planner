# Evaluating a Multi-Agent Personalized Travel Planner for Riyadh

## Project Overview

This project investigates whether a coordinated multi-agent architecture
can improve personalized travel itinerary planning compared with a
single-agent baseline.

The current M4 implementation focuses on a working single-agent
baseline for generating personalized Riyadh travel itineraries.

## User Inputs

The system accepts three structured inputs:

1. Trip Duration: 1 to 5 days in the current interface.
2. Interests: One or more selections from seven predefined categories.
3. Budget Level: Low, Medium, or High.

## Expected Output

For each request, the system generates:

- One hotel for the entire trip.
- Two activities per day.
- Two restaurants per day.

Recommendations are selected from the project's Riyadh datasets.

## Single-Agent Baseline

The baseline uses one Gemini LLM agent with three search tools:

- find_activities
- find_restaurants
- find_hotels

The agent receives the user's structured inputs, calls the search
tools, and generates a structured itinerary.

The current configured model is gemini-3.5-flash-lite.

## Datasets

The project uses three processed datasets:

- data/activities.csv
- data/restaurants.csv
- data/hotels.csv

All recommended places are identified by dataset-specific place IDs.

## Evaluation

The implemented evaluation reports:

- Structural validity
- Activity Preference Match (%)
- Restaurant Budget Match (%)
- Hotel Budget Match
- Geographic coordinate checks
- Mean and maximum pairwise distances between daily places

Geographic distances are straight-line estimates, not road travel
times. Opening-hour and full temporal feasibility checks are not
implemented in this baseline version.

## Running the Project in Google Colab

### Required Files

- `Riyadh_Travel_Planner_M4_Clean.ipynb`
- `riyadh_m4_datasets.zip`
- `requirements.txt`

The dataset ZIP contains the three processed CSV files.

### Setup and Execution

1. Open `Riyadh_Travel_Planner_M4_Clean.ipynb` in Google Colab.
2. Run the first cell to install the Python dependencies.
3. Run the dataset setup cell. In a fresh Colab session,
   upload `riyadh_m4_datasets.zip` when prompted.
4. The notebook extracts the CSV files to
   `/content/riyadh_project/data/`.
5. Create a Gemini API key using Google AI Studio.
6. Open Colab Secrets (key icon in the left sidebar).
7. Add a secret named `GEMINI_API_KEY` and paste the key.
8. Enable notebook access to the secret.
9. Run the remaining notebook cells in order.
10. Open the Gradio interface displayed by the final cell.
11. Select trip duration, interests, and budget level.
12. Click Generate Itinerary to create and evaluate a trip.

### Notes

- An internet connection and a working Gemini API key are required.
- The notebook uses `gemini-3.5-flash-lite`.
- Model requests may be subject to API limits or temporary errors.
- Do not commit API keys, credentials, or Colab secrets.
- The ZIP file is provided to simplify setup in a fresh Colab runtime.

## Current Limitations

- Recommendation quality depends on dataset classifications.
- Some Shopping records represent individual stores rather than
  major tourist shopping destinations.
- Dataset coordinates do not provide actual driving times.
- Hotel coordinates are missing for some records.
- Real-time opening hours and booking availability are not supported.
- Reported match scores are based on the defined dataset labels.

## Project Milestones

M4: Working single-agent baseline and demonstration.

Future milestones will evaluate the baseline systematically and
compare it with the coordinated multi-agent treatment using
controlled inputs, datasets, and evaluation criteria.
