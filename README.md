# Intro-to-AI-Group-9

Structure of the System Architecture of LeafLens

Inputs: A mix of healthy and diseased potato leaves for image detection and analysis

AI Component: Convolutional Neural Networks (CNN), K-Nearest Neighbours (KNN), Supervised Learning

Outputs: Whether the leaf is diseased or not.

SETUP INSTRUCTIONS
 LeafLens — Potato Leaf Disease Detection

Upload a photo of a potato leaf, get a diagnosis: Early Blight, Late
Blight, or Healthy. A CNN trained from scratch (`FINALCNN`) powers the
predictions, served via FastAPI and shown through a web UI.

## Structure

- `Leaf_Lens.ipynb` — trains the model (run in Google Colab)
- `python-service/` — FastAPI backend that serves predictions
- `src/` — frontend (Lovable / TanStack Start)

## Setup

```bash
# Frontend
npm i          # or: bun install

# Backend
cd python-service
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
```

## Run it

1. **Train the model:** open `Leaf_Lens.ipynb` in Google Colab, run all
   cells. This produces `models/leaf_cnn.pt` and starts the backend.
2. **Expose the backend:** the notebook's ngrok cell gives you a public
   URL for it.
3. **Connect the frontend:** set `CNN_API_URL` to that URL — in a local
   `.env` file, or in Lovable under Cloud → Secrets.
4. **Run the frontend:** `npm run dev` (or use the Lovable preview) and
   open it in a browser.

Prefer running the backend locally instead of Colab?
```bash
cd python-service
uvicorn app.main:app --reload --port 8000
```
Then set `CNN_API_URL=http://localhost:8000`.

## Usage example

Upload a leaf photo and click **Diagnose**. You'll get back something like:

```json
{
  "disease": "Early blight",
  "confidence": "high",
  "summary": "The CNN classifies this as early blight on potato with 92% confidence.",
  "topK": [{ "label": "Potato___Early_blight", "probability": 0.92 }]
}
```

Or test the API directly:
```bash
curl http://localhost:8000/health
```

## AI assistance disclosure

Parts of this project (backend bug fixes, notebook debugging, this
README) were developed with help from Claude (Anthropic), per the
course's academic honesty policy.


