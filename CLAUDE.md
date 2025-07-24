### Setup for each new project (You should only need to run this once at the beggining of the project)
1. Do git init ChatUs
2. Instal TDD Guard for both JavaScript/TypeScript: Vitest and Python: pytest
> npm install --save-dev tdd-guard-vitest
> uv add tdd-guard-pytest

### Python Package Management with uv

Use uv exclusively for Python package management in this project.

#### Package Management Commands
- All Python dependencies **must be installed, synchronized, and locked** using uv
- Never use pip, pip-tools, poetry, or conda directly for dependency management

Use these commands:
- Install dependencies: `uv add <package>`
- Remove dependencies: `uv remove <package>`
- Sync dependencies: `uv sync`

#### Running Python Code
- Run a Python script with `uv run <script-name>.py`
- Run Python tools like Pytest with `uv run pytest` or `uv run ruff`
- Launch a Python repl with `uv run python`

#### Managing Scripts with PEP 723 Inline Metadata

- Run a Python script with inline metadata (dependencies defined at the top of the file) with: `uv run script.py`
- You can add or remove dependencies manually from the `dependencies =` section at the top of the script, or
- Or using uv CLI:
    - `uv add package-name --script script.py`
    - `uv remove package-name --script script.py`

### Git Version Control

Use Git for all version control operations in this project. Follow these conventions and best practices.

#### Git Commands and Workflow

##### Basic Operations
- Check status: `git status`
- Stage changes: `git add <file>` or `git add .` for all changes
- Commit changes: `git commit -m "descriptive message"`
- Push to remote: `git push origin <branch-name>`
- Pull latest changes: `git pull origin <branch-name>`

##### Branch Management
- Create and switch to new branch: `git checkout -b <branch-name>`
- Switch branches: `git checkout <branch-name>`
- List branches: `git branch -a`
- Delete local branch: `git branch -d <branch-name>`
- Delete remote branch: `git push origin --delete <branch-name>`

##### Commit Message Convention
Always use clear, descriptive commit messages following this pattern:
- `feat: add new feature`
- `fix: resolve bug in component`
- `docs: update README`
- `refactor: improve code structure`
- `test: add unit tests`
- `chore: update dependencies`

##### Working with Changes
- View differences: `git diff` (unstaged) or `git diff --staged` (staged)
- Undo last commit (keep changes): `git reset --soft HEAD~1`
- Undo changes to a file: `git checkout -- <file>`
- Stash changes temporarily: `git stash` and `git stash pop` to restore
- View commit history: `git log --oneline -10`

##### Collaboration
- Fetch without merging: `git fetch origin`
- Merge branches: `git merge <branch-name>`
- Rebase current branch: `git rebase <branch-name>`
- Cherry-pick a commit: `git cherry-pick <commit-hash>`

#### Important Guidelines

##### Always Do
- Pull before pushing to avoid conflicts
- Create feature branches for new work
- Write meaningful commit messages
- Review changes with `git diff` before committing
- Keep commits atomic (one logical change per commit)

##### Never Do
- Force push to main/master branch: Never use `git push --force` on shared branches
- Commit sensitive data (passwords, API keys, etc.)
- Commit large binary files without Git LFS
- Merge without reviewing changes first
- Work directly on main/master for features

#### Handling Merge Conflicts
When conflicts occur:
1. Pull the latest changes: `git pull origin <branch>`
2. Open conflicted files and resolve manually
3. Stage resolved files: `git add <resolved-files>`
4. Complete the merge: `git commit`

#### Git Configuration
Ensure these are set before committing:
- Set name: `git config user.name "BellamyPT"`
- Set email: `git config user.email "Batista.Rui7@gmail.com"`
- For this project only, add `--local` flag

#### Working with Remote Repositories
- Add remote: `git remote add origin <url>`
- View remotes: `git remote -v`
- Change remote URL: `git remote set-url origin <new-url>`
- Remove remote: `git remote remove <name>`


### 🔄 Project Awareness & Context
- **Always read `PLANNING.md`** at the start of a new conversation to understand the project's architecture, goals, style, and constraints.
- **Check `TASK.md`** before starting a new task. If the task isn’t listed, add it with a brief description and today's date.
- **Use consistent naming conventions, file structure, and architecture patterns** as described in `PLANNING.md`.
- **Use venv_linux** (the virtual environment) whenever executing Python commands, including for unit tests.

### 🧱 Code Structure & Modularity
- **Never create a file longer than 500 lines of code.** If a file approaches this limit, refactor by splitting it into modules or helper files.
- **Organize code into clearly separated modules**, grouped by feature or responsibility.
  For agents this looks like:
    - `agent.py` - Main agent definition and execution logic 
    - `tools.py` - Tool functions used by the agent 
    - `prompts.py` - System prompts
- **Use clear, consistent imports** (prefer relative imports within packages).
- **Use clear, consistent imports** (prefer relative imports within packages).
- **Use python_dotenv and load_env()** for environment variables.

### ✅ Task Completion
- **Mark completed tasks in `TASK.md`** immediately after finishing them.
- Add new sub-tasks or TODOs discovered during development to `TASK.md` under a “Discovered During Work” section.

### 📎 Backend Style & Conventions
- **Use Python** as the primary language.
- **Follow PEP8**, use type hints, and format with `black`.
- **Use `pydantic` for data validation**.
- Use `FastAPI` for APIs and `SQLAlchemy` or `SQLModel` for ORM if applicable.
- Write **docstrings for every function** using the Google style:
  ```python
  def example():
      """
      Brief summary.

      Args:
          param1 (type): Description.

      Returns:
          type: Description.
      """
  ```

### 📎 Frontend Style & Conventions

- **Use React with TypeScript** as the primary framework and language.
- **Follow ESLint rules**, use TypeScript strict mode, and format with `prettier`.
- **Use Tailwind CSS** for all styling - avoid inline styles or CSS modules.
- Use `Vite` as the build tool and `React Router` for routing.
- **Use functional components** with hooks - no class components.
- Write **JSDoc comments for every component** using this style:
  ```tsx
  /**
   * Brief component description.
   * @param {Object} props - Component props
   * @param {string} props.title - The title to display
   * @param {() => void} props.onClick - Click handler function
   * @returns {JSX.Element} Rendered component
   */
  const ExampleComponent = ({ title, onClick }: Props): JSX.Element => {
    return <div>...</div>
  }
  ```

#### Component Structure
- **One component per file** with the same name as the component
- Use **named exports** for components (not default exports)
- Keep components small and focused on a single responsibility
- Organize components in folders by feature/domain

#### State Management
- Use **React hooks** for local state (`useState`, `useReducer`)
- Use **Context API** for cross-component state when needed
- For complex state, consider **Zustand** or **TanStack Query** for server state
- Avoid prop drilling - use composition or context instead

#### TypeScript Conventions
```typescript
// Define prop types as interfaces
interface ComponentProps {
  title: string;
  isActive?: boolean;
  onClick: (id: string) => void;
  children: React.ReactNode;
}

// Use type for unions and intersections
type Status = 'idle' | 'loading' | 'success' | 'error';
```

#### Tailwind CSS Usage
- Use **Tailwind utility classes** exclusively
- Follow mobile-first responsive design: `className="text-sm md:text-base lg:text-lg"`
- Extract repeated class combinations into components, not @apply
- Use **semantic color names** from Tailwind config (e.g., `bg-primary` not `bg-blue-500`)

#### File Naming Conventions
- Components: `PascalCase.tsx` (e.g., `UserProfile.tsx`)
- Hooks: `camelCase` starting with 'use' (e.g., `useAuth.ts`)
- Utilities: `camelCase.ts` (e.g., `formatDate.ts`)
- Types: `PascalCase.types.ts` (e.g., `User.types.ts`)

#### Project Structure
```
src/
├── components/     # Shared/common components
├── features/       # Feature-specific components and logic
├── hooks/          # Custom React hooks
├── utils/          # Utility functions
├── types/          # TypeScript type definitions
├── services/       # API service functions
└── assets/         # Images, fonts, etc.
```

#### Performance Best Practices
- Use **React.memo** for expensive pure components
- Implement **lazy loading** with `React.lazy()` for route components
- Use **useMemo** and **useCallback** hooks appropriately
- Optimize images with proper formats and lazy loading

#### Testing Approach
- Write tests using **Vitest** and **React Testing Library**
- Focus on user behavior, not implementation details
- Maintain test files alongside components: `Component.test.tsx`
- Aim for high coverage of critical user paths

### 📚 Documentation & Explainability
- **Update `README.md`** when new features are added, dependencies change, or setup steps are modified.
- **Comment non-obvious code** and ensure everything is understandable to a mid-level developer.
- When writing complex logic, **add an inline `# Reason:` comment** explaining the why, not just the what.

### 🧠 AI Behavior Rules
- **Never assume missing context. Ask questions if uncertain.**
- **Never hallucinate libraries or functions** – only use known, verified Python packages.
- **Always confirm file paths and module names** exist before referencing them in code or tests.
- **Never delete or overwrite existing code** unless explicitly instructed to or if part of a task from `TASK.md`.