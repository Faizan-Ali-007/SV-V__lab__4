# Delivery Robot — State Model

| State-ID | State Name | Description | Entry Condition | Exit Condition |
|----------|------------|--------------|------------------|------------------|
| S1 | IDLE | Robot is powered on and waiting for a delivery request. | Power-on, OR Warehouse Reached (returning from RETURNING) | Delivery Request Received |
| S2 | NAVIGATING | Robot is moving toward the destination (or back toward the warehouse after avoiding an obstacle). | Delivery Request Received (from IDLE), OR Obstacle Avoided (from AVOIDING_OBSTACLE) | Obstacle Detected, OR Destination Reached, OR Critical Battery |
| S3 | AVOIDING_OBSTACLE | Robot has paused normal navigation to avoid a detected obstacle. | Obstacle Detected (from NAVIGATING) | Obstacle Avoided |
| S4 | DELIVERING | Robot is at the destination, performing the package delivery process. | Destination Reached (from NAVIGATING) | Delivery Successful |
| S5 | RETURNING | Robot is moving back to the warehouse after delivery, or after a critical battery event. | Delivery Successful (from DELIVERING), OR Critical Battery (from NAVIGATING) | Warehouse Reached |

## Events / Conditions
| Event | Description |
|-------|-------------|
| Delivery Request Received | A new delivery task is assigned to the robot. |
| Obstacle Detected | Robot's sensors detect an obstacle in its path. |
| Obstacle Avoided | Robot has successfully maneuvered around the obstacle. |
| Destination Reached | Robot has arrived at the delivery destination. |
| Delivery Successful | Package has been successfully handed off / dropped. |
| Critical Battery | Battery level falls below the safe operating threshold. |
| Warehouse Reached | Robot has arrived back at the warehouse. |
