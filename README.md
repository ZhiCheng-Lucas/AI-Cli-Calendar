# AI CliCalendar

A lightweight, AI-powered command-line calendar that helps you prioritize what truly matters.

## Vision

AI CliCalendar exists to solve a fundamental productivity challenge: deciding what to focus on next. By combining the simplicity of a command-line interface with the intelligence of large language models, it creates a distraction-free environment where your tasks are not just listed, but thoughtfully organized based on their importance, urgency, and your personal context.

## Key Features

### AI-Powered Task Prioritization

The heart of AI CliCalendar is its ability to analyze your tasks through the lens of an AI assistant. When you request a daily plan, it:

- Evaluates task importance based on deadlines, dependencies, and your stated priorities
- Considers your historical work patterns and completion rates
- Identifies potential bottlenecks or conflicts in your schedule
- Recommends a focused, achievable set of priorities for your day

### Adaptive Time Management

Unlike rigid scheduling systems, AI CliCalendar understands that plans change:

- Tracks partial progress on tasks when you can't complete them in one session
- Learns from the difference between estimated and actual completion times
- Adjusts future recommendations based on your demonstrated work capacity
- Provides intelligent suggestions for rescheduling when priorities shift

### Streamlined Interaction

Everything in AI CliCalendar is designed for efficiency:

- Quick command syntax for adding, updating, and completing tasks
- Focused daily views that reduce decision fatigue
- Simple tagging system for organizing related tasks
- Distraction-free interface that keeps you in the flow

## How It Works

1. **Task Collection**: Add tasks through simple CLI commands, including title, description, estimated duration, and any deadlines.

2. **Data Storage**: All information is stored in a single SQLite table on your device, organized to capture task details, priorities, progress, and time tracking.

3. **AI Analysis**: When you request guidance, the application connects to your configured LLM (like DeepSeek).

4. **Context Building**: The system constructs a prompt that includes:
   - Your upcoming deadlines and commitments
   - Tasks you've marked as high priority
   - Your recent productivity patterns and completion rates
   - Available time blocks in your schedule

5. **Prioritization**: The LLM analyzes this context and returns:
   - A ranked list of tasks for your day
   - Suggested time blocks for focused work
   - Reasoning for why certain tasks take precedence
   - Strategies for handling potential challenges

6. **Execution & Feedback**: As you work through tasks, you update their status and progress, creating a feedback loop that improves future recommendations.

## Technical Architecture

```
├── core/
│   ├── calendar.py      # Calendar data management
│   ├── database.py      # SQLite interaction
│   └── llm_connector.py # Interface with language models
├── cli/
│   ├── commands.py      # Command definitions
│   └── display.py       # Terminal output formatting
└── config/
    └── settings.py      # User configuration
```

The database uses a single, carefully designed table to track all necessary task information:

```sql
CREATE TABLE tasks (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    title TEXT NOT NULL,
    description TEXT,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    due_date DATETIME,
    start_time DATETIME,
    end_time DATETIME,
    duration_minutes INTEGER,
    user_priority INTEGER,
    ai_priority INTEGER,
    status TEXT DEFAULT 'pending',
    progress_percent INTEGER DEFAULT 0,
    time_spent_minutes INTEGER DEFAULT 0,
    completed_at DATETIME,
    recurring BOOLEAN DEFAULT 0,
    recurrence_pattern TEXT,
    tags TEXT,
    notes TEXT
);
```

## Project Status

This project is currently in active development.

## License

MIT
