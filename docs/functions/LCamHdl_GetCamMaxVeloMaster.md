# LCamHdl_GetCamMaxVeloMaster

## Principle of operation

The function LCamHdl_GetCamMaxVeloMaster calculates the maximum possible
master velocity with respect to the given maximum dynamics(velocity, acceleration and jerk) of the following axis and the cam following values (min. and max first, second and third derivatives).

Prerequisite is, that the cam disk is used at a constant master velocity - accelerations or decelerations of the master axis are not taken into account. The time base of the master and slave axis must be equal (e.g. seconds).

The minimum and maximum following value derivatives can be determined with the function block LCamHdl_GetCamFollowingMinMax.

The function calculates the maximum master velocity using the following equations:

```math
v_{MasterMax_v} = \frac{s\rq}{v_{LimitSlave}} \newline
v_{MasterMax_a} = \sqrt{\frac{s\rq\rq}{a_{LimitSlave}}} \newline
v_{MasterMax_j} = \left(\frac{s\rq\rq\rq}{j_{LimitSlave}}\right)^{1/3}
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
| `maxSlaveVelocity` | `LREAL` | Maximum permissible velocity of the slave axis |
| `maxSlaveAcceleration` | `LREAL` | Maximum permissible acceleration of the slave axis |
| `maxSlaveJerk` | `LREAL` | Maximum permissible jerk of the slave axis, ignored if <= 0.0 |

### Output Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `maxMasterVelocity` | `LREAL` | Maximum permissible velocity of the master axis to not exceed the maximum slave axis dynamics |
