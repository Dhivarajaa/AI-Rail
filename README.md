✨ Features
Interactive Train Scheduling:

Manually add custom trains with specific types, priorities, arrival windows, and dwell times.

Instantly load pre-defined, real-world train schedules for major Indian railway junctions (Erode, Chennai, Bangalore, Mumbai, Delhi, Howrah).

Simple Traffic Optimizer:

A greedy, earliest-deadline-first scheduling algorithm assigns trains to a configurable number of tracks (sections) to minimize conflicts.

In-Browser Machine Learning (with TensorFlow.js):

Generate Synthetic Data: Create a sample dataset for training a delay-risk prediction model.

Train Live: Train a simple neural network directly in your browser.

Predict Risk: Use the trained model to predict a "delay risk" score (Low, Med, High) for each custom-added train.

AI Railway Assistant:

A rule-based chatbot that answers common questions about Indian Railways trains (e.g., Rajdhani, Shatabdi), station codes, and coach classes (1A, 2A, SL, etc.).

Modern UI & Visualization:

A clean, dark-themed interface to display schedules, optimization results, and model status.

Responsive design that works on various screen sizes.

Action logs to track user-initiated events.

🛠️ How It Works
This project is built as a single index.html file with no external dependencies other than the TensorFlow.js CDN.

1. Scheduling Engine
The core scheduling logic uses a greedy, earliest-deadline-first algorithm. It sorts all custom trains first by their arrival window (arr) and then by their priority (descending). It then iterates through the sorted list, assigning each train to the earliest available track that can accommodate its dwell time within the defined simulation horizon. Trains that cannot be scheduled are marked as 'UNSCHEDULED'.

2. In-Browser ML Model
The application leverages TensorFlow.js to demonstrate a delay prediction model without needing a server.

Generate Data: Clicking "Generate Data" creates a synthetic dataset where a "risk" label is heuristically calculated based on features like arrival time, train priority, and dwell time.

Train Model: A small sequential neural network (with two hidden relu layers and a final sigmoid output layer) is defined and trained on the synthetic data. The training progress (epoch and loss) is displayed live.

Predict Risks: Once trained, the model can infer a "delay risk" score for each user-added train based on its features ([priority, arr, dwell, length]).

3. AI Assistant
The "AI Railway Assistant" is a simulated chatbot. It operates on a rule-based system, matching keywords in the user's input (e.g., 'erode', 'rajdhani', '1a') to provide pre-written, informative responses. It does not use a large language model but effectively demonstrates the user-facing part of an AI system.

🚀 How to Run
No setup, server, or build steps are required!

Download the Code:

Clone the repository:

Bash

git clone https://github.com/your-username/your-repo-name.git
Or, simply download the index.html file.

Open in Browser:

Navigate to the project folder and open the index.html file in a modern web browser (like Google Chrome, Mozilla Firefox, or Microsoft Edge).

That's it! The application is now running locally.

💻 Tech Stack
Frontend: HTML5, CSS3 (with CSS Variables for theming), Vanilla JavaScript (ES6+)

Machine Learning: TensorFlow.js

graph TD
    A[Start Application] --> B{User Action};

    B -- Add Train Manually --> C[Input Train Details];
    C --> D{Custom Train Data};
    D --> E[Display Custom Schedule];
    E --> F{Request Optimizer?};
    F -- Yes --> G[Run Greedy Scheduler];
    G --> H[Update Schedule View with Assignments];
    G --> I{Request ML Prediction?};

    B -- Load Junction Schedule --> J[Select Junction (Erode, Chennai, etc.)];
    J --> K[Retrieve Pre-defined Train Data];
    K --> L[Display Junction Schedule];
    L --> F;

    B -- Generate Synthetic ML Data --> M[Create Synthetic Features & Labels];
    M --> N[Update ML Status];
    N --> O{Train Model?};

    O -- Yes --> P[Train TensorFlow.js Model];
    P --> Q[Update ML Status with Loss/Epoch];
    Q --> R{Model Trained?};
    R -- Yes --> I;

    I -- Yes --> S[Predict Risk for Custom Trains];
    S --> T[Update Custom Schedule with Risk Scores];
    T --> E;
    I -- No --> E;

    B -- AI Assistant Chat --> U[User Inputs Chat Message];
    U --> V[Process Message (Keyword Matching)];
    V --> W[Generate AI Response];
    W --> X[Display Chat Messages];
    X --> B;

    B -- Clear All Data --> Y[Reset Trains & Schedule];
    Y --> E;

    B -- Any Other Action --> Z[Process Other Controls/Input];
    Z --> B;

    H --> I;

    T --> B;
    L --> B;
    E --> B;
    N --> B;
    P --> B;
    Q --> B;
    Y --> B;

    subgraph AI/ML Pipeline
        M
        P
        S
    end

    subgraph User Interaction
        C
        J
        U
        Y
        Z
    end

    subgraph Scheduling
        G
        H
    end

    subgraph Display
        E
        K
        L
        T
        W
        X
    end

1. System Architecture Block Diagram
This diagram provides a high-level overview of the main components and the flow of data between them. It shows how user actions trigger processing logic, which in turn updates the data and the final display.

                  +--------------------------------+
                  |         👤 USER INPUTS         |
                  | (Clicks, Text Entry, Selections) |
                  +--------------------------------+
                                  |
                                  | (Triggers Actions)
                                  v
+-------------------------------------------------------------------------+
|                        🖥️ MAIN APPLICATION (In-Browser)                     |
|                                                                         |
|   +--------------------------+     +-------------------------------+    |
|   |      💾 DATA STORAGE       | <-->|      ⚙️ PROCESSING LOGIC        |    |
|   | (JavaScript Variables)   |     |                               |    |
|   |                          |     |  +-------------------------+  |    |
|   | o Custom Train List      | ----> |   Scheduler Engine      |  |    |
|   | o Loaded Junction Data   | <---- | (Assigns tracks)        |  |    |
|   | o TF.js Model State      |     |  +-------------------------+  |    |
|   |                          |     |                               |    |
|   |                          |     |  +-------------------------+  |    |
|   |                          | ----> |   ML Pipeline (TF.js)   |  |    |
|   |                          | <---- | (Trains & Predicts Risk)|  |    |
|   |                          |     |  +-------------------------+  |    |
|   |                          |     |                               |    |
|   |                          |     |  +-------------------------+  |    |
|   |                          | ----> |   AI Assistant Logic    |  |    |
|   |                          | <---- | (Matches keywords)      |  |    |
|   |                          |     |  +-------------------------+  |    |
|   +--------------------------+     +-------------------------------+    |
|                                                                         |
+-------------------------------------------------------------------------+
                                  |
                                  | (Updates Display)
                                  v
                  +--------------------------------+
                  |        📊 UI DISPLAY / OUTPUTS       |
                  |  (Schedule View, Chat, Logs)   |
                  +--------------------------------+
