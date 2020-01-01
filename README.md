# computed_torque_controller

## computed_torque_controller/ComputedTorqueController
### <u>Formulation</u>
The controller expects a general rigid body dynamics system, whose equations of motion are given in the form below.

<img src="https://latex.codecogs.com/gif.latex?M(q)\ddot{q}+C(q,\dot{q})+g(q)=\tau" />

where q, M, C, and g are the joint position vector, inertia matrix, Colioris vector, and gravity vector.

The controller computes the joint effort commands to track the desired joint positions with complensation for the inertia, Colioris, and gravity forces.

<img src="https://latex.codecogs.com/gif.latex?\tau_d=M(q)(\ddot{q}+PID(q_d))+C(q,\dot{q})+g(q)" />

### <u>Prerequisites</u>
* robot description in URDF to build a dynamics model (using dart::utils::DartLoader)
* hardware_interface/JointStateHandle for all joints appeared in the model
* hardware_interface/EffortJointHandle for controlled joints specified by the controller param

### <u>Subscribed topics</u>
___<controller_namespace>/<joint_name>/command___ (std_msgs/Float64)
* Position command for each controlled joint

### <u>Parameters</u>
___<controller_namespace>/robot_description___ or ___robot_description___ (string, required)
* robot description in URDF

___<controller_namespace>/joints/<joint_name>___ (struct, required)
* control_toolbox::Pid

```
computed_torque_conotroller:
    type: computed_torque_controller/ComputedTorqueController
    joints:
        joint_a:
            p: 1.
            i: 1.
            d: 1.
            publish_state: true
        joint_b:
            ...
```