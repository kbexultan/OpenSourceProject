Contributing to SAVEAT

Thank you for your interest in contributing to SAVEAT! Every bug report, idea, and pull request helps make the project better.

How to Contribute
Fork the repository.
Clone your fork and create a new branch from main:
bash
git checkout -b feature/short-description
Make your changes and test them locally.
Commit your changes with a clear message.
Push the branch to your fork.
Open a Pull Request to main and describe what you changed and why.
Project Structure
backend/: server-side application and database logic.
frontend/: web application.
mobile/: mobile application.

Please keep your changes within the relevant part of the project and follow the existing structure.

Local Setup

Each part of the project has its own setup steps, described in the README. Private settings (database credentials, JWT secrets, API keys) belong in environment variables. Never commit your .env files.

Code Guidelines
Write clean, readable code.
Follow the existing code style and project structure.
Use clear, descriptive names for variables and functions.
Add or update tests when your change affects behavior.
Update the documentation if needed.
Never upload passwords, API keys, tokens, or private environment files.
Branch and Commit Messages
Branch names: feature/..., fix/..., docs/....
Write commit messages in the imperative mood, for example Fix cart restoration bug or Add food expiry filter.
Keep each commit focused on one change.
Pull Request Checklist

Before submitting, please make sure that:

[ ] The code runs and the tests pass.
[ ] The change is focused and does not include unrelated edits.
[ ] No secrets or private files are included.
[ ] Documentation is updated where necessary.
Reporting Issues

Found a bug or have an idea? Open an Issue in the GitHub repository. For bugs, please include:

steps to reproduce,
expected and actual behavior,
your environment (OS, browser or device, app version) and screenshots if possible.
Code of Conduct

All contributors must follow our Code of Conduct.

License

By contributing, you agree that your contributions will be licensed under the project's LICENSE.

Thank you for helping improve SAVEAT!
