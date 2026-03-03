# Tech Pack Logo Placement Tool

A Streamlit web app for placing logos on cap images with perspective warping and generating professional **trucker hat tech pack** PDF reports. Supports Excel design data, multiple cap views, and AI-generated placement descriptions.

## Features

- **Excel integration** — Upload an Excel file and select a data range (key/value columns) to include fabric & design details in the PDF.
- **Logo placement** — Draw a 4-corner polygon on the cap image to place your logo with realistic perspective warp (OpenCV).
- **Multiple cap views** — Add several cap images (e.g. front, side, back), each with its own logo placement.
- **AI descriptions** — Optional OpenAI (GPT-4o-mini) descriptions for each placement; falls back to a simple text description if no API key is set.
- **PDF report** — Generate a single tech pack PDF with design details, cap images, and a logo placement summary table.

## Prerequisites

- **Python 3.8+**
- **OpenAI API key** (optional) — Set `OPENAI_API_KEY` in your environment for AI-generated placement descriptions. The app works without it using fallback text.

## Installation

1. Clone or download this repository.
2. Create a virtual environment (recommended):

   ```bash
   python -m venv venv
   venv\Scripts\activate   # Windows
   # source venv/bin/activate   # macOS/Linux
   ```

3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. (Optional) Set your OpenAI API key:

   ```bash
   set OPENAI_API_KEY=your-key-here   # Windows
   # export OPENAI_API_KEY=your-key-here   # macOS/Linux
   ```

## Usage

1. Start the app:

   ```bash
   streamlit run app.py
   ```

2. In the browser:
   - **Step 0:** Upload your Excel file and set the key/value column names and row range, then click **Fetch Data from Excel**.
   - **Step 1:** Upload your logo image (PNG/JPG).
   - **Step 2:** Enter approximate logo width and height in cm (for the report text).
   - **Step 3:** Upload a cap/base image. Draw a **4-point polygon** in clockwise order (Top-Left → Top-Right → Bottom-Right → Bottom-Left), then **double-click the 4th point** to finalize. Adjust the placement description and click **Save This Cap**.
   - Repeat Step 3 for more cap views if needed.
   - Use **Generate PDF Report** to create the tech pack, then **Download Techpack PDF**.

Outputs are saved in the `outputs/` folder (images and `logo_techpack.pdf`).

## Project Structure

| File / folder      | Description |
|--------------------|-------------|
| `app.py`           | Main Streamlit UI and workflow. |
| `opencv_logic.py`  | Perspective warp: applies logo onto cap image using 4 corner points. |
| `ai_part.py`       | AI description generation (OpenAI) and PDF report building (ReportLab); used by `app.py`. |
| `ai_part2.py`      | Alternative CLI-style flow with AI and PDF (standalone). |
| `requirements.txt` | Python dependencies. |
| `uploads/`         | Created at runtime for uploaded files. |
| `outputs/`         | Created at runtime for generated images and PDF. |

## Excel Format

- The app reads columns by **1-based row range** and uses columns **1 and 2** (B and C) by default for key/value pairs.
- You specify the **column names** in the UI (e.g. "Detail", "Value") and the **start/end row** to include in the tech pack’s “Fabric & Design Details” table.

## License

Use and modify as needed for your project.
