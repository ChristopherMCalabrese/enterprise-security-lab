# Project 07 - Intelligent Presence Automation
## Status

🟡 In Progress

## Objective

Build an event-driven presence automation platform using a Raspberry Pi 5, Home Assistant, n8n, and an Everything Presence Pro sensor.

The system is designed to detect changes in physical presence, transport those events between systems, evaluate the event using workflow logic, and eventually control connected devices or services automatically.

The initial use case is presence-based lighting automation, but the architecture is intentionally designed to support additional automation scenarios.

Why This Project Matters

Modern home automation increasingly depends on reliable presence detection rather than simple motion sensors or manually triggered actions.

This project provides an opportunity to study event-driven architecture, API integration, webhooks, workflow automation, and physical sensor data while building a practical automation platform.

Rather than connecting every device directly to every other device, the architecture separates responsibilities between the presence sensor, Home Assistant, and n8n.

This creates a flexible foundation that can support additional automation and security workflows in the future.

## Learning Objectives
Build an event-driven automation workflow.
Integrate physical presence detection with Home Assistant.
Integrate Home Assistant with n8n.
Use REST APIs and webhooks to exchange events between systems.
Implement conditional workflow logic.
Develop reliable presence-based automation.
Evaluate and tune presence detection behavior.
Apply security controls to automation infrastructure.
Document an integrated IoT and automation architecture.
Technologies
Implemented
Raspberry Pi 5
Home Assistant
n8n
Everything Presence Pro
Home Assistant REST Command
Home Assistant Automation
n8n Webhook
n8n IF node
HTTP Request nodes
REST API integration
Planned
Presence sensor tuning
Presence persistence testing
Delayed occupancy-off logic
Physical lighting integration
Additional presence-based automations
Expanded workflow logic
Architecture

The system uses an event-driven architecture in which presence information flows from the physical sensor through Home Assistant into n8n.

                    +----------------------+
                    |  Everything Presence |
                    |        Pro           |
                    +----------+-----------+
                               |
                         Presence Event
                               |
                               v
                    +----------------------+
                    |   Home Assistant     |
                    |                      |
                    | Event / Automation   |
                    +----------+-----------+
                               |
                          REST / HTTP
                               |
                               v
                    +----------------------+
                    |     n8n Workflow     |
                    |                      |
                    | Webhook → IF → Action|
                    +----------+-----------+
                               |
                         API / HTTP
                               |
                               v
                    +----------------------+
                    |   Automation /       |
                    |   External Service   |
                    +----------------------+

The exact network addressing, hostnames, authentication credentials, webhook URLs, and management details are intentionally omitted from this public documentation.

Presence Detection

The project uses an Everything Presence Pro sensor to provide multiple presence-related signals.

The sensor provides several detection capabilities, including:

Occupancy
mmWave Presence
Motion
Static Presence
Tracking Presence
Zone Presence

The initial automation uses the Occupancy entity as the primary event source.

The sensor is currently undergoing tuning and validation before the automation is considered production-ready.

Home Assistant Integration

Home Assistant acts as the event source and automation platform for the presence sensor.

A Home Assistant automation monitors changes to the occupancy state.

When the occupancy state changes, Home Assistant invokes a REST command that sends the event to the n8n production webhook.

The event contains:

Entity identifier
Current occupancy state

This allows n8n to process the event without requiring direct access to the physical sensor.

n8n Integration

n8n acts as the workflow orchestration layer.

The workflow contains:

Webhook trigger
Conditional IF node
HTTP request for the on state
HTTP request for the off state

The workflow evaluates the occupancy state and routes the event accordingly.

Conceptually:

Presence Event
      |
      v
   Webhook
      |
      v
     IF
   /    \
 on      off
 |        |
 v        v
Action   Action

This architecture allows additional processing and decision-making to be added without modifying the underlying presence sensor.

Security

The automation platform was configured with security and privacy considerations in mind.

Security measures include:

Authentication between Home Assistant and n8n.
Production webhook used for active automation.
n8n public API disabled.
n8n diagnostics/telemetry disabled.
Unverified package installation disabled.
DNS filtering used to control unwanted external communication.
Automation services remain behind the internal network security boundary.

Credentials and authentication tokens are never stored in public documentation.

Implementation
Phase 1 — n8n Deployment

n8n was deployed on the Raspberry Pi 5 using Docker.

A reverse proxy provides HTTPS access to the n8n interface.

The deployment was validated using Docker Compose configuration and container health checks.

Phase 2 — Home Assistant API Integration

Home Assistant API connectivity was validated independently before integrating it with n8n.

The API was confirmed to respond correctly when authenticated using a Home Assistant access token.

The token itself was never stored in documentation or exposed to the workflow development process.

Phase 3 — n8n Webhook

A webhook workflow was created in n8n to receive presence events from Home Assistant.

The initial implementation used the n8n test webhook during development.

After validation, the workflow was published and transitioned to the production webhook.

Phase 4 — Conditional Workflow

An IF node was added to evaluate the presence state.

The workflow compares the incoming state against:

on

Events matching on follow the TRUE branch.

Events matching off follow the FALSE branch.

Both paths were manually tested before connecting the workflow to the production Home Assistant automation.

Phase 5 — Home Assistant Automation

A Home Assistant automation was created using the Everything Presence Pro Occupancy entity as the trigger.

The automation invokes a REST command that sends the entity identifier and current state to n8n.

This creates the complete event path:

Everything Presence Pro
        |
        v
Home Assistant
        |
        v
REST Command
        |
        v
n8n Production Webhook
        |
        v
IF Condition
        |
     +--+--+
     |     |
    ON    OFF
Validation

The system has been manually validated at each stage.

Validation included:

Presence sensor state changes observed in Home Assistant.
Home Assistant automation successfully triggered.
Home Assistant REST command successfully configured.
n8n test webhook successfully received events.
on state successfully routed through the TRUE branch.
off state successfully routed through the FALSE branch.
Home Assistant API requests successfully authenticated.
HTTP service requests completed successfully.
Production n8n webhook published successfully.
Real sensor state changes successfully triggered the Home Assistant automation.

The physical lighting hardware has not yet been installed, so final physical actuator validation remains outstanding.

Current State

The event pipeline is operational:

Everything Presence Pro
        ↓
Home Assistant
        ↓
n8n Production Webhook
        ↓
IF State Evaluation
        ↓
ON / OFF Action

The infrastructure and workflow integration have been validated.

The primary remaining task is tuning the presence sensor and developing more robust occupancy logic before relying on the system for permanent lighting control.

Challenges
n8n DNS Resolution

During initial n8n troubleshooting, external telemetry DNS resolution was failing.

Investigation confirmed that DNS filtering was intentionally sinkholing the telemetry domain.

Normal external DNS resolution continued to function, confirming that general container networking was operational.

Telemetry was subsequently disabled in n8n because it was not required for the intended deployment.

Home Assistant Connectivity

Initial connectivity testing showed that the Home Assistant API was reachable but required authentication.

A Home Assistant access token was created and tested independently before being used by n8n.

This confirmed API connectivity without exposing credentials within the workflow documentation.

Test vs Production Webhooks

The n8n workflow initially used a test webhook while the workflow was being developed.

After successful testing, the workflow was published and transitioned to the production webhook.

This distinction is important because the test endpoint requires the workflow to be actively listening, while the production endpoint operates when the workflow is published.

Presence Sensor Behavior

The Everything Presence Pro provides multiple detection signals, and the initial Occupancy entity may require additional tuning before it is suitable for reliable lighting automation.

The next stage of the project is therefore focused on observing:

Detection speed
False positives
False negatives
Persistence while stationary
Time required to transition to unoccupied
Behavior when partially obstructed
Differences between Occupancy, Motion, Static Presence, and Tracking Presence
Future Improvements

The next version of the automation should avoid immediately turning a device off when presence temporarily disappears.

A more reliable design would be:

Presence Detected
       |
       v
    Light ON
       |
       v
Presence Lost
       |
       v
   Wait Period
       |
       v
Re-check Presence
       |
   +---+---+
   |       |
Present   Empty
   |       |
   v       v
Keep     Light OFF
Light
ON

This reduces the impact of temporary sensor state changes and provides a better user experience.

Additional future improvements may include:

Presence timeout configuration
Multi-sensor correlation
Zone-based automation
Time-of-day logic
Manual override support
Notification workflows
Additional Home Assistant device integrations
Security-related automation
Environmental automation
n8n error handling and retry logic
Lessons Learned

Event-driven automation is significantly more flexible than tightly coupling individual devices together.

Separating responsibilities between Home Assistant and n8n allows each platform to focus on its strengths.

Home Assistant provides device integration and real-time state information, while n8n provides workflow orchestration, conditional logic, API integration, and extensibility.

The project also reinforced the importance of validating each integration independently before combining multiple systems.

Testing the Home Assistant API, n8n webhook, conditional logic, and final automation separately made troubleshooting significantly easier.

Finally, reliable automation requires more than a technically functional workflow. Sensor behavior must be observed and tuned under realistic conditions before automation can be considered production-ready.

Skills Demonstrated
Raspberry Pi administration
Docker deployment
n8n workflow development
Home Assistant automation
IoT integration
Presence detection
REST API integration
Webhook development
Event-driven architecture
Conditional workflow design
Network troubleshooting
DNS troubleshooting
Authentication management
Automation security
Infrastructure documentation
System integration
Technical troubleshooting
