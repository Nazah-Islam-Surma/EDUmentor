# Implementation Plan: AI-Powered Educational Platform

## Overview

This implementation plan breaks down the AI-powered educational platform into manageable steps. The platform will be built using TypeScript/Node.js for the backend services and React/TypeScript for the frontend. We'll start with core functionality and progressively add features.

The implementation follows a layered approach:
1. Set up project infrastructure and data models
2. Build core services (Teacher Agent, Mentor Agent, Sessions)
3. Implement AI/ML integrations
4. Create API layer and authentication
5. Build client interfaces
6. Add advanced features (proactive reminders, progress tracking)

## Tasks

- [ ] 1. Project Setup and Infrastructure
  - Create project directory structure with separate folders for backend services, frontend, and shared types
  - Initialize TypeScript configuration for both backend and frontend
  - Set up package.json with dependencies (Express, React, TypeScript, testing libraries)
  - Configure ESLint and Prettier for code quality
  - Set up testing framework (Jest) with fast-check for property-based testing
  - Create Docker configuration for local development
  - _Requirements: All (foundational)_

- [ ] 2. Database Schema and Data Models
  - [ ] 2.1 Define core TypeScript interfaces and types
    - Create Student, TeacherAgent, MentorAgent, Session interfaces
    - Create LearningProfile, ProgressData, Subscription interfaces
    - Create supporting types (Message, StudyRoutine, ClassNotes, etc.)
    - _Requirements: 1.1, 4.1, 9.1, 11.1_
  
  - [ ] 2.2 Set up database connection and ORM
    - Configure PostgreSQL database connection
    - Set up Prisma or TypeORM as ORM
    - Create database migration scripts
    - _Requirements: All (data persistence)_
  
  - [ ] 2.3 Implement database models and schemas
    - Create database schemas for all core entities
    - Add indexes for performance optimization
    - Set up foreign key relationships
    - _Requirements: All (data persistence)_
  
  - [ ]* 2.4 Write property test for data model integrity
    - **Property 1: Teacher Agent Creation Completeness**
    - **Validates: Requirements 1.1, 1.5**

- [ ] 3. Content Processing Service
  - [ ] 3.1 Implement file upload handler
    - Create endpoint to accept PDF, video, and book files
    - Validate file types and sizes
    - Store files in cloud storage (S3 or similar)
    - _Requirements: 1.2_
  
  - [ ] 3.2 Build PDF text extraction
    - Use pdf-parse library to extract text from PDFs
    - Handle multi-page documents
    - Extract metadata (title, author, page count)
    - _Requirements: 1.2, 1.3_
  
  - [ ] 3.3 Build video transcription
    - Integrate with speech-to-text service (e.g., AWS Transcribe, Google Speech-to-Text)
    - Extract audio from video files
    - Generate timestamped transcripts
    - _Requirements: 1.2, 1.3, 7.2_
  
  - [ ] 3.4 Implement knowledge extraction
    - Parse extracted text to identify key concepts
    - Extract topics and create concept definitions
    - Build searchable knowledge base structure
    - _Requirements: 1.3, 7.3, 7.4_
  
  - [ ]* 3.5 Write property test for training material processing
    - **Property 2: Training Material Processing**
    - **Validates: Requirements 1.2, 1.3**
  
  - [ ]* 3.6 Write unit tests for content processing
    - Test PDF extraction with sample files
    - Test error handling for corrupted files
    - Test unsupported file format rejection
    - _Requirements: 1.2, 1.3_

- [ ] 4. Checkpoint - Verify content processing works
  - Ensure all tests pass, ask the user if questions arise.

- [ ] 5. Teacher Agent Service
  - [ ] 5.1 Implement teacher agent creation
    - Create function to instantiate new teacher agents
    - Assign unique IDs and initialize empty knowledge base
    - Configure education level and subject
    - _Requirements: 1.1, 1.4_
  
  - [ ] 5.2 Integrate LLM for Socratic teaching
    - Set up connection to LLM API (OpenAI GPT-4 or Anthropic Claude)
    - Create prompt templates for Socratic method
    - Implement question generation logic
    - _Requirements: 2.1, 2.2_
  
  - [ ] 5.3 Build response evaluation system
    - Analyze student responses for comprehension
    - Generate follow-up questions based on understanding
    - Track struggling vs. mastered concepts
    - _Requirements: 2.3, 2.5_
  
  - [ ] 5.4 Implement adaptive teaching logic
    - Adjust questioning difficulty based on student performance
    - Provide hints when student struggles repeatedly
    - Progress to advanced material when mastery demonstrated
    - _Requirements: 3.3, 3.4, 12.3, 12.4_
  
  - [ ]* 5.5 Write property test for Socratic response generation
    - **Property 3: Socratic Response Generation**
    - **Validates: Requirements 2.1, 2.4**
  
  - [ ]* 5.6 Write property test for difficulty adjustment
    - **Property 14: Difficulty Adjustment**
    - **Validates: Requirements 12.3, 12.4**
  
  - [ ]* 5.7 Write unit tests for teacher agent
    - Test agent creation with various configurations
    - Test response generation for sample questions
    - Test error handling when LLM is unavailable
    - _Requirements: 1.1, 2.1, 2.2_

- [ ] 6. Session Management Service
  - [ ] 6.1 Implement session lifecycle management
    - Create function to start new teaching sessions
    - Track session state (active, paused, ended)
    - Generate unique session IDs
    - _Requirements: 3.1_
  
  - [ ] 6.2 Build message handling system
    - Handle text-based messages between student and agent
    - Store message history in session
    - Support real-time message delivery
    - _Requirements: 3.2, 3.5_
  
  - [ ] 6.3 Implement session progress tracking
    - Track topics covered during session
    - Calculate comprehension level based on interactions
    - Identify struggling and mastered concepts
    - _Requirements: 3.6, 11.1_
  
  - [ ] 6.4 Build session persistence
    - Save session data when session ends
    - Store progress updates to database
    - Make session history retrievable
    - _Requirements: 3.6_
  
  - [ ]* 6.5 Write property test for session progress persistence
    - **Property 4: Session Progress Persistence**
    - **Validates: Requirements 3.6**
  
  - [ ]* 6.6 Write unit tests for session management
    - Test session creation and termination
    - Test message handling and storage
    - Test progress calculation accuracy
    - _Requirements: 3.1, 3.2, 3.6_

- [ ] 7. Checkpoint - Verify teaching sessions work end-to-end
  - Ensure all tests pass, ask the user if questions arise.

- [ ] 8. Mentor Agent Service - Core Features
  - [ ] 8.1 Implement mentor agent assignment
    - Create function to assign mentor to student
    - Link mentor to student's subscription
    - Initialize mentor with student's learning profile
    - _Requirements: 4.1_
  
  - [ ] 8.2 Build class note-taking system
    - Capture audio/video stream from class
    - Transcribe class content using speech-to-text
    - Structure notes with timestamps
    - _Requirements: 4.3, 7.1, 7.2_
  
  - [ ] 8.3 Implement note processing and organization
    - Extract key points from transcripts
    - Identify and categorize topics
    - Organize notes by subject and relevance
    - Make notes accessible to student
    - _Requirements: 4.4, 7.3, 7.4, 7.5_
  
  - [ ]* 8.4 Write property test for class notes transcription
    - **Property 8: Class Notes Transcription**
    - **Validates: Requirements 7.2, 7.3, 7.4**
  
  - [ ]* 8.5 Write unit tests for note-taking
    - Test transcription with sample audio
    - Test key point extraction
    - Test topic identification
    - _Requirements: 7.2, 7.3, 7.4_

- [ ] 9. Study Routine Creation
  - [ ] 9.1 Implement learning pattern analysis
    - Analyze student's session history
    - Identify learning pace and preferences
    - Calculate available study time from profile
    - _Requirements: 6.1, 6.2_
  
  - [ ] 9.2 Build study routine generator
    - Create personalized schedule based on analysis
    - Allocate time across all subjects
    - Prioritize topics based on curriculum and struggles
    - _Requirements: 4.5, 6.2_
  
  - [ ] 9.3 Implement routine update logic
    - Monitor student progress continuously
    - Adjust routine when student struggles or masters topics
    - Reallocate study time dynamically
    - _Requirements: 6.3, 6.4_
  
  - [ ]* 9.4 Write property test for study routine creation
    - **Property 6: Study Routine Creation**
    - **Validates: Requirements 6.1, 6.2**
  
  - [ ]* 9.5 Write property test for study routine updates
    - **Property 15: Study Routine Updates**
    - **Validates: Requirements 6.3, 6.4**
  
  - [ ]* 9.6 Write unit tests for study routines
    - Test routine generation with various learning profiles
    - Test routine updates after progress changes
    - Test edge cases (no available time, single subject)
    - _Requirements: 6.1, 6.2, 6.3_

- [ ] 10. Proactive Reminder System
  - [ ] 10.1 Implement reminder scheduler
    - Create background job to check scheduled study times
    - Trigger reminders at appropriate times
    - Handle time zones correctly
    - _Requirements: 5.1_
  
  - [ ] 10.2 Build multi-channel notification system
    - Implement text message sending (Twilio or similar)
    - Implement voice call capability
    - Implement push notifications
    - _Requirements: 5.2_
  
  - [ ] 10.3 Implement reminder content generation
    - Generate contextual reminder messages
    - Include what needs to be studied
    - Personalize based on student preferences
    - _Requirements: 5.5_
  
  - [ ] 10.4 Build follow-up logic
    - Track missed study sessions
    - Send follow-up reminders
    - Adjust frequency based on responsiveness
    - _Requirements: 5.3, 5.4_
  
  - [ ]* 10.5 Write property test for proactive reminder delivery
    - **Property 7: Proactive Reminder Delivery**
    - **Validates: Requirements 5.1, 5.2**
  
  - [ ]* 10.6 Write unit tests for reminders
    - Test reminder scheduling accuracy
    - Test multi-channel delivery
    - Test follow-up logic
    - _Requirements: 5.1, 5.2, 5.3_

- [ ] 11. Checkpoint - Verify mentor features work
  - Ensure all tests pass, ask the user if questions arise.

- [ ] 12. Subscription Management Service
  - [ ] 12.1 Implement subscription CRUD operations
    - Create function to create new subscriptions
    - Implement subscription update and cancellation
    - Support multiple subscription tiers
    - _Requirements: 9.1, 9.2_
  
  - [ ] 12.2 Build access control system
    - Check subscription status before granting feature access
    - Implement feature gating by subscription tier
    - Handle expired subscriptions gracefully
    - _Requirements: 9.3, 9.4_
  
  - [ ] 12.3 Implement subscription notifications
    - Track subscription expiration dates
    - Send notifications before expiration
    - Notify on successful renewal
    - _Requirements: 9.5_
  
  - [ ] 12.4 Build renewal and upgrade system
    - Allow subscription renewal
    - Support tier upgrades and downgrades
    - Handle payment processing integration
    - _Requirements: 9.6_
  
  - [ ]* 12.5 Write property test for subscription access control
    - **Property 10: Subscription Access Control**
    - **Validates: Requirements 9.3, 9.4**
  
  - [ ]* 12.6 Write property test for mentor availability
    - **Property 5: Mentor Availability**
    - **Validates: Requirements 4.2**
  
  - [ ]* 12.7 Write unit tests for subscription management
    - Test subscription creation and updates
    - Test access control with various tiers
    - Test expiration handling
    - _Requirements: 9.1, 9.2, 9.3, 9.4_

- [ ] 13. Progress Tracking System
  - [ ] 13.1 Implement progress data recording
    - Record performance data from all sessions
    - Track time spent per subject and topic
    - Count completed sessions
    - _Requirements: 11.1_
  
  - [ ] 13.2 Build progress metrics calculation
    - Calculate comprehension levels per topic
    - Calculate overall subject progress
    - Track study streaks and achievements
    - _Requirements: 11.2_
  
  - [ ] 13.3 Implement topic status management
    - Mark topics as not started, in progress, struggling, completed, mastered
    - Update status based on session outcomes
    - Track mastery dates
    - _Requirements: 11.4_
  
  - [ ] 13.4 Build progress visualization data
    - Generate time-series data for progress over time
    - Create subject-wise progress summaries
    - Prepare data for charts and graphs
    - _Requirements: 11.3_
  
  - [ ]* 13.5 Write property test for progress tracking accuracy
    - **Property 12: Progress Tracking Accuracy**
    - **Validates: Requirements 11.1, 11.2**
  
  - [ ]* 13.6 Write unit tests for progress tracking
    - Test progress calculation with sample session data
    - Test topic status transitions
    - Test achievement tracking
    - _Requirements: 11.1, 11.2, 11.4_

- [ ] 14. Learning Personalization System
  - [ ] 14.1 Implement learning style detection
    - Monitor student interactions to identify patterns
    - Detect visual, auditory, kinesthetic, or reading/writing preferences
    - Update learning profile with detected style
    - _Requirements: 12.1, 12.5_
  
  - [ ] 14.2 Build adaptive teaching method selector
    - Choose teaching approaches based on learning style
    - Adjust content presentation format
    - Modify explanation strategies
    - _Requirements: 12.2_
  
  - [ ] 14.3 Implement alternative explanation system
    - Generate multiple explanation approaches for concepts
    - Try different methods when student struggles
    - Track which approaches work best
    - _Requirements: 12.4_
  
  - [ ]* 14.4 Write property test for learning style adaptation
    - **Property 13: Learning Style Adaptation**
    - **Validates: Requirements 12.2**
  
  - [ ]* 14.5 Write unit tests for personalization
    - Test learning style detection
    - Test teaching method adaptation
    - Test alternative explanation generation
    - _Requirements: 12.1, 12.2, 12.4_

- [ ] 15. Education Level Adaptation
  - [ ] 15.1 Implement language complexity analyzer
    - Calculate readability scores for generated content
    - Measure vocabulary complexity
    - Assess sentence structure complexity
    - _Requirements: 8.2_
  
  - [ ] 15.2 Build level-appropriate content generator
    - Adjust language for children, primary, secondary, high school, college
    - Simplify or sophisticate vocabulary based on level
    - Adapt teaching pace and depth
    - _Requirements: 8.1, 8.2_
  
  - [ ] 15.3 Implement multi-level student support
    - Allow students to interact with agents at different levels
    - Track progress separately per level
    - _Requirements: 8.3_
  
  - [ ]* 15.4 Write property test for education level adaptation
    - **Property 9: Education Level Adaptation**
    - **Validates: Requirements 8.2**
  
  - [ ]* 15.5 Write unit tests for level adaptation
    - Test content generation for each education level
    - Test readability score calculations
    - Test vocabulary complexity adjustments
    - _Requirements: 8.1, 8.2_

- [ ] 16. Checkpoint - Verify personalization and adaptation
  - Ensure all tests pass, ask the user if questions arise.

- [ ] 17. Avatar Rendering Engine
  - [ ] 17.1 Set up avatar rendering framework
    - Choose avatar rendering library (Ready Player Me, or custom with Three.js)
    - Initialize 3D rendering engine
    - Set up avatar asset pipeline
    - _Requirements: 1.5, 10.1_
  
  - [ ] 17.2 Implement avatar creation and customization
    - Create avatars with configurable appearance
    - Support different styles (realistic, cartoon, professional)
    - Allow customization of hair, eyes, skin tone
    - _Requirements: 10.2, 10.5_
  
  - [ ] 17.3 Build facial expression animation
    - Implement expression types (happy, neutral, thinking, encouraging)
    - Animate transitions between expressions
    - Sync expressions with conversation context
    - _Requirements: 10.3_
  
  - [ ] 17.4 Implement lip-sync system
    - Integrate text-to-speech for audio generation
    - Synchronize lip movements with speech audio
    - Ensure latency under 100ms
    - _Requirements: 10.4_
  
  - [ ]* 17.5 Write property test for avatar lip sync
    - **Property 11: Avatar Lip Sync**
    - **Validates: Requirements 10.4**
  
  - [ ]* 17.6 Write unit tests for avatar rendering
    - Test avatar creation with various configurations
    - Test expression animation
    - Test lip-sync timing accuracy
    - _Requirements: 10.1, 10.2, 10.3, 10.4_

- [ ] 18. Voice and Speech Integration
  - [ ] 18.1 Implement text-to-speech service
    - Integrate with TTS API (Google Cloud TTS, Amazon Polly, or ElevenLabs)
    - Support multiple voices and languages
    - Generate natural-sounding speech
    - _Requirements: 3.5_
  
  - [ ] 18.2 Implement speech-to-text service
    - Integrate with STT API (Google Speech-to-Text, AWS Transcribe)
    - Handle real-time audio streaming
    - Support multiple languages
    - _Requirements: 3.5_
  
  - [ ] 18.3 Build voice session handler
    - Manage voice-based teaching sessions
    - Handle audio input/output streams
    - Convert between text and voice seamlessly
    - _Requirements: 3.5_
  
  - [ ]* 18.4 Write unit tests for voice integration
    - Test TTS with sample text
    - Test STT with sample audio
    - Test voice session flow
    - _Requirements: 3.5_

- [ ] 19. API Layer and Authentication
  - [ ] 19.1 Set up Express API server
    - Create Express application
    - Configure middleware (CORS, body parser, compression)
    - Set up routing structure
    - _Requirements: All (API access)_
  
  - [ ] 19.2 Implement authentication system
    - Set up JWT-based authentication
    - Create login and registration endpoints
    - Implement password hashing (bcrypt)
    - _Requirements: All (security)_
  
  - [ ] 19.3 Build authorization middleware
    - Implement role-based access control
    - Create middleware to check subscription status
    - Protect routes based on permissions
    - _Requirements: 9.3, 9.4_
  
  - [ ] 19.4 Create API endpoints for all services
    - Teacher agent endpoints (create, upload materials, start session)
    - Mentor agent endpoints (assign, attend class, create routine)
    - Session endpoints (create, send message, end)
    - Subscription endpoints (create, update, cancel)
    - Progress endpoints (get progress, get history)
    - _Requirements: All_
  
  - [ ]* 19.5 Write integration tests for API
    - Test authentication flow
    - Test authorization checks
    - Test all major API endpoints
    - _Requirements: All_

- [ ] 20. Checkpoint - Verify API layer works
  - Ensure all tests pass, ask the user if questions arise.

- [ ] 21. Frontend - Core UI Components
  - [ ] 21.1 Set up React application
    - Create React app with TypeScript
    - Configure routing (React Router)
    - Set up state management (Redux or Context API)
    - Configure API client (Axios)
    - _Requirements: All (user interface)_
  
  - [ ] 21.2 Build authentication UI
    - Create login page
    - Create registration page
    - Implement authentication state management
    - Add protected route wrapper
    - _Requirements: All (user access)_
  
  - [ ] 21.3 Create student dashboard
    - Display active subscriptions
    - Show upcoming study sessions
    - Display progress overview
    - Provide quick access to teachers and mentor
    - _Requirements: 6.5, 11.3_
  
  - [ ] 21.4 Build teacher selection interface
    - List available teacher agents
    - Display teacher subjects and levels
    - Allow starting teaching sessions
    - _Requirements: 1.1, 3.1_
  
  - [ ] 21.5 Create teaching session interface
    - Build chat interface for text-based sessions
    - Display teacher avatar
    - Show conversation history
    - Handle real-time message updates
    - _Requirements: 3.2, 3.5_

- [ ] 22. Frontend - Advanced Features
  - [ ] 22.1 Build mentor interface
    - Display mentor avatar
    - Show study routine
    - Access class notes
    - Chat with mentor
    - _Requirements: 4.2, 6.5, 7.5_
  
  - [ ] 22.2 Create progress tracking dashboard
    - Display progress charts and graphs
    - Show subject-wise progress
    - Display topic status (mastered, struggling, etc.)
    - Show achievements and study streaks
    - _Requirements: 11.2, 11.3_
  
  - [ ] 22.3 Build study routine viewer
    - Display personalized study schedule
    - Show upcoming study sessions
    - Allow marking sessions as complete
    - _Requirements: 6.5_
  
  - [ ] 22.4 Create subscription management UI
    - Display current subscription status
    - Show available tiers and features
    - Allow upgrading/downgrading
    - Handle renewal
    - _Requirements: 9.1, 9.2, 9.6_
  
  - [ ] 22.5 Build admin interface for educators
    - Create teacher agents
    - Upload training materials
    - View student progress
    - Manage subscriptions
    - _Requirements: 1.1, 1.2_

- [ ] 23. Frontend - Voice and Avatar Integration
  - [ ] 23.1 Integrate avatar rendering in UI
    - Embed avatar renderer in session interface
    - Display animated avatars during conversations
    - Handle avatar loading and errors
    - _Requirements: 10.1, 10.3, 10.4_
  
  - [ ] 23.2 Implement voice session UI
    - Add microphone input controls
    - Display audio waveform visualization
    - Show transcription in real-time
    - Handle voice session state
    - _Requirements: 3.5_
  
  - [ ]* 23.3 Write UI component tests
    - Test major components render correctly
    - Test user interactions
    - Test error states
    - _Requirements: All (UI)_

- [ ] 24. Error Handling and Resilience
  - [ ] 24.1 Implement global error handling
    - Create error handling middleware for API
    - Implement error boundaries in React
    - Log errors to monitoring service
    - _Requirements: All (reliability)_
  
  - [ ] 24.2 Build retry and fallback logic
    - Retry failed LLM requests with exponential backoff
    - Provide fallback responses when AI unavailable
    - Auto-reconnect on connection loss
    - _Requirements: 3.2, 4.2_
  
  - [ ] 24.3 Implement graceful degradation
    - Allow session completion even if subscription expires
    - Provide limited features when services unavailable
    - Save progress before errors occur
    - _Requirements: 9.4_
  
  - [ ]* 24.4 Write unit tests for error handling
    - Test error middleware
    - Test retry logic
    - Test fallback responses
    - _Requirements: All (reliability)_

- [ ] 25. Performance Optimization
  - [ ] 25.1 Implement caching layer
    - Cache frequently accessed knowledge bases
    - Cache student learning profiles
    - Use Redis for session data
    - _Requirements: All (performance)_
  
  - [ ] 25.2 Optimize database queries
    - Add database indexes
    - Implement query result caching
    - Use connection pooling
    - _Requirements: All (performance)_
  
  - [ ] 25.3 Optimize frontend performance
    - Implement code splitting
    - Lazy load components
    - Optimize avatar rendering for mobile
    - Compress assets
    - _Requirements: All (user experience)_

- [ ] 26. Security Hardening
  - [ ] 26.1 Implement input validation
    - Validate all API inputs
    - Sanitize user-generated content
    - Prevent SQL injection and XSS
    - _Requirements: All (security)_
  
  - [ ] 26.2 Add rate limiting
    - Implement rate limiting per user
    - Add IP-based rate limiting
    - Protect against DDoS
    - _Requirements: All (security)_
  
  - [ ] 26.3 Implement data encryption
    - Encrypt sensitive student data at rest
    - Use TLS 1.3 for all communications
    - Secure API keys and secrets
    - _Requirements: All (privacy)_
  
  - [ ] 26.4 Add content safety filters
    - Filter inappropriate AI responses
    - Monitor and log all AI interactions
    - Implement parental controls
    - _Requirements: All (safety)_

- [ ] 27. Deployment and DevOps
  - [ ] 27.1 Create Docker containers
    - Dockerize backend services
    - Dockerize frontend application
    - Create docker-compose for local development
    - _Requirements: All (deployment)_
  
  - [ ] 27.2 Set up CI/CD pipeline
    - Configure automated testing
    - Set up automated deployment
    - Implement staging environment
    - _Requirements: All (deployment)_
  
  - [ ] 27.3 Configure cloud infrastructure
    - Set up Kubernetes cluster
    - Configure load balancers
    - Set up database instances
    - Configure object storage
    - _Requirements: All (deployment)_
  
  - [ ] 27.4 Set up monitoring and logging
    - Configure Prometheus for metrics
    - Set up Grafana dashboards
    - Configure ELK stack for logging
    - Set up alerts for critical issues
    - _Requirements: All (operations)_

- [ ] 28. Final Integration and Testing
  - [ ] 28.1 Perform end-to-end integration testing
    - Test complete user flows
    - Test teacher session flow
    - Test mentor interaction flow
    - Test subscription flow
    - _Requirements: All_
  
  - [ ] 28.2 Conduct performance testing
    - Load test API endpoints
    - Test concurrent user sessions
    - Measure response times
    - _Requirements: All (performance)_
  
  - [ ] 28.3 Verify all correctness properties
    - Run all property-based tests
    - Ensure 100+ iterations per property
    - Fix any failing properties
    - _Requirements: All_

- [ ] 29. Final Checkpoint - System ready for deployment
  - Ensure all tests pass, ask the user if questions arise.

## Notes

- Tasks marked with `*` are optional and can be skipped for faster MVP
- Each task references specific requirements for traceability
- Checkpoints ensure incremental validation at major milestones
- Property tests validate universal correctness properties across all inputs
- Unit tests validate specific examples, edge cases, and error conditions
- The implementation uses TypeScript for type safety and better developer experience
- Start with core features (tasks 1-11) for a working MVP, then add advanced features
- For a non-CSE student: Focus on understanding one task at a time, use the design document as reference, and don't hesitate to ask questions at checkpoints
