```mermaid
graph TB
    %% =================================================
    %% INITIAL ENTRY & CLASSIFICATION
    %% =================================================
    START([Client Input]) --> CLASSIFY{Input Classification}

    %% =================================================
    %% STAGE 1: SAFETY BUILDING
    %% =================================================
    subgraph "Stage 1: Safety Building"
        %% Substate 1.1: Goal and Vision
        subgraph "1.1 Goal and Vision"
            G1["1.1a: Initial Goal Inquiry"]
            G2["1.1b: Goal Clarification"]
            G3["1.1c: Vision Building"]
            G4["1.1d: Vision Acceptance"]
        end

        %% Substate 1.2: Problem and Body
        subgraph "1.2 Problem and Body"
            P1["1.2a: Problem Inquiry"]
            P2["1.2b: Body Symptom Focus"]
            P3["1.2c: Present Moment Body"]
            P4["1.2d: Pattern Recognition"]
        end

        %% Substate 1.3: Readiness Assessment
        subgraph "1.3 Readiness Assessment"
            R1["1.3a: Safety Check"]
            R2["1.3b: Rapport Assessment"]
            R3["1.3c: Intervention Readiness"]
            R4["1.3d: Stage Completion"]
        end
    end

    %% =================================================
    %% FLOWS & CONNECTIONS
    %% =================================================

    %% --- Classification Decision Points ---
    CLASSIFY --> |Vague Goal| G1
    CLASSIFY --> |Clear Goal| G2
    CLASSIFY --> |External Blame| REDIRECT1[/Redirect to Internal/]
    CLASSIFY --> |Crisis Indicators| CRISIS[Crisis Stabilization]
    CLASSIFY --> |Trauma Surfaces| TRAUMA[Trauma Stabilization]

    %% --- 1.1 Goal and Vision Flow ---
    G1 --> |Ask Clarifying Questions| G1_OUT{Client Response}
    G1_OUT --> |Still Vague| G1
    G1_OUT --> |Goal Stated| G2
    G2 --> |Explore Future Self| G3
    G3 --> |Build the Vision| G3_OUT{Vision Response}
    G3_OUT --> |Vision Rejected| G3
    G3_OUT --> |Vision Accepted| G4
    G4 --> |Check Completion| ADVANCE1{1.1 Complete?}

    %% --- 1.2 Problem and Body Flow ---
    P1 --> |Ask About Problem| P1_OUT{Problem Response}
    P1_OUT --> |External Focus| REDIRECT2[/Redirect to Internal/]
    P1_OUT --> |Body Symptoms| P2
    P1_OUT --> |Emotional Pattern| P4
    P2 --> |Explore Body Awareness| P3
    P3 --> |Focus on Present Moment| P3_OUT{Body Awareness}
    P3_OUT --> |Aware of Body| P4
    P3_OUT --> |In Analysis Mode| REDIRECT3[/Shift Thinking to Feeling/]
    P4 --> |Explore Pattern| P4_OUT{Pattern Response}
    P4_OUT --> |Pattern Understood| ADVANCE2{1.2 Complete?}
    P4_OUT --> |Needs More Exploration| P1

    %% --- 1.3 Readiness Assessment Flow ---
    R1 --> |Check for Safety| R1_OUT{Safety Response}
    R1_OUT --> |Safe to Proceed| R2
    R1_OUT --> |Safety Concerns| STAY_SAFE[Stay in Safety Building]
    R2 --> |Assess Rapport| R2_OUT{Rapport Response}
    R2_OUT --> |Good Rapport| R3
    R2_OUT --> |Needs More Safety| R1
    R3 --> |Assess Readiness| R3_OUT{Readiness Response}
    R3_OUT --> |Ready for Intervention| R4
    R3_OUT --> |Needs More Exploration| P1
    R4 --> |Stage 1 Complete| TRANSITION[Transition to Stage 2]

    %% --- Advancement & Loop Logic ---
    ADVANCE1 --> |Goal & Vision ✓| P1
    ADVANCE1 --> |Incomplete| G1
    ADVANCE2 --> |Problem & Body ✓| R1
    ADVANCE2 --> |Incomplete| P1

    %% --- Redirect & Stabilization Flows ---
    REDIRECT1 --> |Shift Focus| G1
    REDIRECT2 --> |Shift Focus| P1
    REDIRECT3 --> |Shift Modality| P3
    CRISIS --> |Stabilized| G1
    TRAUMA --> |Stabilized| G1

    %% --- Final Transition ---
    TRANSITION --> STAGE2([Stage 2: Change Logical Levels])

    %% =================================================
    %% STYLING - WITH DARK TEXT
    %% =================================================
    %% --- Style Definitions ---
    classDef goalState fill:#cce5ff,stroke:#66a3ff,stroke-width:2px,color:#333;
    classDef problemState fill:#e6ccff,stroke:#b366ff,stroke-width:2px,color:#333;
    classDef readinessState fill:#d4edda,stroke:#5cb85c,stroke-width:2px,color:#333;
    classDef decisionPoint fill:#fff3cd,stroke:#ffc107,stroke-width:2px,color:#333;
    classDef criticalState fill:#f8d7da,stroke:#d9534f,stroke-width:2px,color:#333;
    classDef redirectState fill:#e2e3e5,stroke:#6c757d,stroke-width:2px,color:#333;
    classDef transitionState fill:#d1ecf1,stroke:#007bff,stroke-width:2px,color:#333;
    classDef startEndStyle fill:#6c757d,stroke:#343a40,stroke-width:2px,color:#fff;

    %% --- Assigning Styles to Nodes ---
    class START,STAGE2 startEndStyle;
    class G1,G2,G3,G4 goalState;
    class P1,P2,P3,P4 problemState;
    class R1,R2,R3,R4 readinessState;
    class CLASSIFY,G1_OUT,G3_OUT,P1_OUT,P3_OUT,P4_OUT,R1_OUT,R2_OUT,R3_OUT,ADVANCE1,ADVANCE2 decisionPoint;
    class CRISIS,TRAUMA,STAY_SAFE criticalState;
    class REDIRECT1,REDIRECT2,REDIRECT3 redirectState;
    class TRANSITION transitionState;
