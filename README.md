# data622 - Assignment 4 Overview

### Collaborators:
Haig Bedros, Noori Selina, Julia Ferris, Matthew Roland

### Project Overview
`overview to be added here`

# Team Collaboration Guidelines for Python Project

## 1. Clone the Repository
Before starting, ensure you have Git installed. Clone the repository to your local machine:

```bash
git clone <repository-url>
cd <repository-name>
```

## 2. Set Up the Virtual Environment
### Create and Activate the Environment
- **Windows:**
  ```bash
  python -m venv .venv
  venv\Scripts\activate
  ```

- **macOS/Linux:**
  ```bash
  python -m venv .venv
  source .venv/bin/activate
  ```

## 3. Install Dependencies
Install the required libraries as specified in the `requirements.txt` file:

```bash
pip install -r requirements.txt
```

## 4. Launch Jupyter Notebook
Start Jupyter Notebook to work on the project:

```bash
jupyter notebook
```

## 5. Project Structure
Familiarize yourself with the project structure:
```
your-repo-name/
│
├── data/               # Store datasets here
├── notebooks/          # Jupyter notebooks for analysis
├── scripts/            # Python scripts
├── requirements.txt    # List of dependencies
├── README.md           # Project documentation
└── venv/               # Virtual environment (not to be pushed)
```

## 6. Working on Notebooks
- Create or edit Jupyter Notebooks in the `notebooks/` folder.
- Use markdown cells for documentation and explanations.
- Save your work frequently.

## 7. Committing Changes
Before making changes, ensure you pull the latest updates:

```bash
git pull origin main  # or your branch name
```

### Commit Your Changes
After completing your work, add and commit your changes:

```bash
git add .
git commit -m "Brief description of changes"
```

### Push Changes
Push your changes to the repository:

```bash
git push origin main  # or your branch name
```

## 8. Using Issues and Pull Requests
- Use GitHub Issues to track tasks and discuss features or bugs.
- For significant changes, create a new branch, push it to the repository, and submit a Pull Request for review.

## 9. Documentation and Communication
- Keep the `README.md` updated with relevant information about the project.
- Communicate regularly with the team through comments in notebooks and GitHub discussions.

## 10. Exit the Virtual Environment
When finished working, deactivate the virtual environment:

```bash
deactivate
```
