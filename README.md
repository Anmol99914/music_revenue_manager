## Music Revenue Manager (MRM) 

A web platform that helps independent musicians, producers, and collaborators manage music revenue, expenses, royalty agreements, and settlements in one place, replacing error-prone spreadsheets.

#### Status: Early development (academic project).

#### Technology Stack
Backend: Python and Django
Frontend: Django Templates
Styling: Tailwind CSS
Interactivity: HTMX (when required)
Database: PostgreSQL
Financial calculations: Python Decimal
Version Control: Git and GitHub

#### MVP Scope
User authentication and basic project roles
Project and track management
Contributor management
Project-level royalty agreements
Revenue recording
Single-payer project expenses
Basic royalty calculation and expense recoupment
Reimbursement tracking
Settlement generation and full-payment recording
Basic financial summaries

#### Advanced features such as track-specific agreements, custom expense allocation, multiple expense payers, individual advances, partial settlements, and agreement versioning are planned for Phase 2.

### Getting Started
bash
git clone https://github.com/Anmol99914/music_revenue_manager.git
cd music_revenue_manager

python -m venv mrm
mrm\Scripts\activate        # Windows
source mrm/bin/activate   # macOS / Linux

pip install -r requirements.txt
python manage.py migrate
python manage.py runserver

Then open http://127.0.0.1:8000.

#### Documentation
Product Requirements
Workflows
Business Rules
