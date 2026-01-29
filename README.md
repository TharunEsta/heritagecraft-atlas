# Heritage Atlas
## Geographical Indication–Based Artisan Commerce Platform

Heritage Atlas is a digital marketplace focused on preserving and promoting India's GI-tagged traditional art forms. The platform organizes artisan products geographically, allowing users to explore crafts based on cultural regions rather than generic product categories.

## Features

- 🗺️ **Map-Centric UI**: Explore crafts by geographical regions
- 🎨 **GI-Tagged Products**: Products organized by Geographical Indications (e.g., Kondapalli, Kalamkari)
- 🔍 **Region-Based Discovery**: Fast filtering using MongoDB aggregation pipelines
- 📸 **Artisan Uploads**: Simple product upload with regional identifiers
- 📖 **Cultural Storytelling**: Rich narratives about traditional art forms
- 🚀 **High Performance**: Optimized queries using MongoDB aggregation

## Tech Stack

- **Frontend**: Modern Web Technologies
- **Backend**: FastAPI
- **Database**: MongoDB (with Aggregation Pipeline)
- **Cloud**: Vercel (Frontend), Render (Backend)

## Project Structure

```
HeritageCraft Atlas/
├── backend/          # FastAPI backend
├── frontend/         # ReactJS frontend
└── README.md
```

## Getting Started

### Prerequisites

- Python 3.9+
- Node.js 18+
- MongoDB (local or MongoDB Atlas)

### Quick Start

1. **Clone the repository:**
```bash
git clone <repository-url>
cd "HeritageCraft Atlas"
```

2. **Backend Setup:**
```bash
cd backend
python -m venv venv
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

pip install -r requirements.txt

# Create .env file from .env.example
cp .env.example .env
# Edit .env with your MongoDB connection string

# Start the backend server
uvicorn main:app --reload
```

The backend API will be available at `http://localhost:8000`
- API Documentation: http://localhost:8000/docs

3. **Seed Sample Data (Optional):**
```bash
cd backend
python seed_data.py
```

4. **Frontend Setup:**
```bash
cd frontend
npm install

# Create .env file from .env.example
cp .env.example .env
# Edit .env with your backend API URL (default: http://localhost:8000)

# Start the frontend development server
npm start
```

The frontend will open at `http://localhost:3000`

## Environment Variables

### Backend (.env)
```
MONGODB_URI=mongodb://localhost:27017/heritagecraft
DATABASE_NAME=heritagecraft
CORS_ORIGINS=http://localhost:3000
```

### Frontend (.env)
```
REACT_APP_API_URL=http://localhost:8000
```

## Deployment

- **Frontend**: Deploy to Vercel
- **Backend**: Deploy to Render

## Objectives

- ✅ Digitally preserve GI-tagged arts
- ✅ Enable region-based product discovery
- ✅ Support artisan-first commerce
- ✅ Use aggregation for high-performance filtering
- ✅ Promote cultural storytelling
- ✅ Enable future e-commerce integrations
- ✅ Encourage fair visibility for rural artists
