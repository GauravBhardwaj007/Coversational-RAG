'''mermaid
graph TB
    %% Initial Entry
    START([Client Input]) --> CLASSIFY{Input Classification<br/>System}

    %% Stage 1 Substates
    subgraph "Stage 1: Safety Building"
        %% Substate 1.1: Goal and Vision
        subgraph "1.1 Goal and Vision"
            G1[1.1a: Initial Goal Inquiry]
            G2[1.1b: Goal Clarification]
            G3[1.1c: Vision Building]
            G4[1.1d: Vision Acceptance]
        end

        %% Substate 1.2: Problem and Body
        subgraph "1.2 Problem and Body"
            P1[1.2a: Problem Inquiry]
            P2[1.2b: Body Symptom Focus]
            P3[1.2c: Present Moment Body]
            P4[1.2d: Pattern Recognition]
        end

        %% Substate 1.3: Readiness Assessment
        subgraph "1.3 Readiness Assessment"
            R1[1.3a: Safety Check]
            R2[1.3b: Rapport Assessment]
            R3[1.3c: Intervention Readiness]
            R4[1.3d: Stage Completion]
        end
    end

    %% Classification Decision Points
    CLASSIFY --> |vague_goal| G1
    CLASSIFY --> |clear_goal| G2
    CLASSIFY --> |external_blame| REDIRECT1{Redirect to Internal}
    CLASSIFY --> |crisis_indicators| CRISIS[Crisis Stabilization]
    CLASSIFY --> |trauma_surfaces| TRAUMA[Trauma Stabilization]

    %% 1.1 Goal and Vision Flow
    G1 --> |RAG: dr_q_goal_clarification| G1_OUT{Client Response}
    G1_OUT --> |still_vague| G1
    G1_OUT --> |goal_stated| G2

    G2 --> |RAG: dr_q_future_self_vision| G3
    G3 --> |RAG: dr_q_vision_building| G3_OUT{Vision Response}
    G3_OUT --> |vision_rejected| G3
    G3_OUT --> |vision_accepted| G4
    G4 --> |completion_check| ADVANCE1{1.1 Complete?}

    %% 1.2 Problem and Body Flow
    P1 --> |RAG: dr_q_problem_inquiry| P1_OUT{Problem Response}
    P1_OUT --> |external_focus| REDIRECT2{Redirect Internal}
    P1_OUT --> |body_symptoms_mentioned| P2
    P1_OUT --> |emotional_pattern| P4

    P2 --> |RAG: dr_q_body_awareness| P3
    P3 --> |RAG: dr_q_present_moment| P3_OUT{Body Awareness}
    P3_OUT --> |present_body_aware| P4
    P3_OUT --> |analysis_mode| REDIRECT3{Thinking→Feeling}

    P4 --> |RAG: dr_q_how_do_you_know| P4_OUT{Pattern Response}
    P4_OUT --> |pattern_understood| ADVANCE2{1.2 Complete?}
    P4_OUT --> |need_more_exploration| P1

    %% 1.3 Readiness Assessment Flow
    R1 --> |RAG: dr_q_safety_check| R1_OUT{Safety Response}
    R1_OUT --> |safe_to_proceed| R2
    R1_OUT --> |safety_concerns| STAY_SAFE[Stay in Safety Building]

    R2 --> |RAG: dr_q_rapport_check| R2_OUT{Rapport Response}
    R2_OUT --> |good_rapport| R3
    R2_OUT --> |need_more_safety| R1

    R3 --> |RAG: dr_q_readiness_assessment| R3_OUT{Readiness Response}
    R3_OUT --> |ready_for_intervention| R4
    R3_OUT --> |need_more_exploration| P1

    R4 --> |stage_1_complete| TRANSITION[Transition to Stage 2]

    %% Advancement Logic
    ADVANCE1 --> |goal✓ AND vision✓| P1
    ADVANCE1 --> |incomplete| G1

    ADVANCE2 --> |problem✓ AND body✓| R1
    ADVANCE2 --> |incomplete| P1

    %% Redirect Flows
    REDIRECT1 --> |RAG: external_to_internal| G1
    REDIRECT2 --> |RAG: external_to_internal| P1
    REDIRECT3 --> |RAG: analysis_to_feeling| P3

    %% Crisis/Trauma Flows
    CRISIS --> |stabilized| G1
    TRAUMA --> |stabilized| G1

    %% Final Transition
    TRANSITION --> STAGE2([Stage 2: Change Logical Levels])

    %% Styling
    classDef goalState fill:#e1f5fe
    classDef problemState fill:#f3e5f5
    classDef readinessState fill:#e8f5e8
    classDef decisionPoint fill:#fff3e0
    classDef criticalState fill:#ffebee
    classDef transitionState fill:#f1f8e9

    class G1,G2,G3,G4 goalState
    class P1,P2,P3,P4 problemState
    class R1,R2,R3,R4 readinessState
    class CLASSIFY,G1_OUT,G3_OUT,P1_OUT,P3_OUT,P4_OUT,R1_OUT,R2_OUT,R3_OUT,ADVANCE1,ADVANCE2 decisionPoint
    class CRISIS,TRAUMA,STAY_SAFE criticalState
    class TRANSITION,STAGE2 transitionState
    '''
    
