# LCamHdl_GetCamMaxSlaveDynamics

## Principle of operation

The function `LCamHdl_GetCamMaxSlaveDynamics` calculates the resulting
maximum following (slave) axis velocity, acceleration and jerk with respect to the
given master velocity and the cam following values (min. and max of first, second
and third derivatives).

Prerequisite is, that the cam disk is used at a constant master velocity -
accelerations or decelerations of the master axis are not taken into account. The
time base of the master and slave axis must be equal (e.g. seconds).

The minimum and maximum following value derivatives can be determined with the
function block `LCamHdl_GetCamFollowingMinMax`.

The function calculates the maximum output values using the following equations:

```math
v_{Slave} = s\rq \cdot v_{Master} \newline
a_{Slave} = s\rq\rq \cdot v_{Master}^2 \newline
j_{Slave} = s\rq\rq\rq \cdot v_{Master}^3
```

$𝑠\rq$ - following axis first derivative (min / max) <br>
$𝑠\rq\rq$ - following axis second derivative (min / max) <br>
$𝑠\rq\rq\rq$ - following axis third derivative (min / max)

## Interface

### Input Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `firstDerivativeMin` | `LREAL` | Cam following value first derivative minimum |
| `firstDerivativeMax` | `LREAL` | Cam following value first derivative maximum |
| `secondDerivativeMin` | `LREAL` | Cam following value second derivative minimum |
| `secondDerivativeMax` | `LREAL` | Cam following value second derivative maximum |
| `thirdDerivativeMin` | `LREAL` | Cam following value third derivative minimum |
| `thirdDerivativeMax` | `LREAL` | Cam following value third derivative maximum |
| `masterVelocity` | `LREAL` | Master velocity |

### Output Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `maxSlaveVelocity` | `LREAL` | Maximum slave velocity |
| `maxSlaveAcceleration` | `LREAL` | Maximum slave acceleration |
| `maxSlaveJerk` | `LREAL` | Maximum slave jerk |
