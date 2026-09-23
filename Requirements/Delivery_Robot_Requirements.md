# Delivery Robot — Requirements

| Req | Description | Priority |
|-----|--------------|----------|
| R1 | The robot shall remain in IDLE state after power-on until a delivery request is received. | High |
| R2 | Upon receiving a delivery request, the robot shall transition from IDLE to NAVIGATING and begin moving toward the destination. | High |
| R3 | While in NAVIGATING state, the robot shall continuously scan its surroundings for obstacles. | High |
| R4 | If an obstacle is detected during navigation, the robot shall suspend normal navigation and transition to AVOIDING_OBSTACLE state. | High |
| R5 | Once an obstacle has been successfully avoided, the robot shall transition back to NAVIGATING and resume movement toward the destination. | High |
| R6 | Upon reaching the destination while NAVIGATING, the robot shall transition to DELIVERING and begin the delivery process. | High |
| R7 | After the package is successfully delivered, the robot shall transition from DELIVERING to RETURNING and begin moving back to the warehouse. | High |
| R8 | The robot shall continuously monitor its battery level while NAVIGATING. | Medium |
| R9 | If the battery level becomes critically low during NAVIGATING, the robot shall abort the current delivery journey and transition to RETURNING. | Critical |
| R10 | Upon reaching the warehouse while RETURNING, the robot shall transition to IDLE and become available for the next delivery request. | High |

## Behavioral Restrictions
- The robot shall never transition directly from IDLE to DELIVERING.
- The robot shall never transition into DELIVERING while in AVOIDING_OBSTACLE state.
