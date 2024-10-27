# lcls-twincat-math

The basic math functions and operations that come with TwinCAT and IEC 61131-3 are limited in scope and complexity.
This repository contains useful mathematical functions for use in TwinCAT projects.
For examples of function block and function syntax, look in the [Test](lcls-twincat-math/lcls_twincat_math/Test) folder.

## Interfaces, Functions and Function Blocks Available
### Interfaces
#### I_Quat
- An interface representing the basic data needed to describe a quaternion of the form: q = w + xi + yj + zk
- Where i, j, and k are defined as:
  - i<sup>2</sup> = j<sup>2</sup> = k<sup>2</sup> = -1
  - ij = k, jk = i, ki = j
  - ji = -k, kj = -i, ik = -j
#### I_Vec3
- An interface representing the basic data needed to describe a 3D vector of the form: v = xi + yj + zk
- Where, i, j, and k are the 3 dimensional unit vectors [1, 0, 0], [0, 1, 0], and [0, 0, 1] respectively. 
### Function Blocks
#### FB_Quaternion
- A function block used to represent a quaternion.
- It implements the I_Quat interface and a number of common functions that can be performed on quaternions:
  - AddQuat
  - DivQuat
  - DivScalar
  - EqualsQuat
  - GetNorm
  - GetNormSq
  - MakeConj
  - MulQuat
  - Normalize
  - Set
  - ToString
- Note that some quaternion operations are not commutative, and the look of how a function is called is intended to show the relative order of operations.
- Additionally, the methods of FB_Quaternion generally update the values stored in the FB_Quaternion while the function equivalents return a copy of an FB_Quaternion with the result.
##### Examples
- Right multiply quaternion 1 by quaternion 2 and store the result in quaternion 1.<br>
`fbQuaternion1.MulQuat(fbQuaternion2);`  
- Right multiply quaternion 1 by quaternion 2 and return a copy of the result. Quaternion 1 and Quaternion 2 are unchanged.<br>
`fbQuaternion3 := F_MulQuat(fbQuaternion1, fbQuaternion2);`  
#### FB_Vec3
- A function block used to represent a 3 dimensional vector.
- It implements the I_Vec3 interface and the I_Quat interface, so it can be used in the quaternion functions as a quaternion with w = 0 or in the Vec3 functions. It also implements a number of common functions that can be performed on an FB_Vec3:
  - AddVec3
  - CrossVec3
  - DivScalar
  - EqualsVec3
  - GetNorm
  - GetNormSq
  - Normalize
  - Set
  - ToString
- Note that the cross product is not commutative, and the look of how the function is called is intended to show the relative order of operations.
- Additionally, the methods of FB_Vec3 generally update the values stored in the FB_Vec3 while the function equivalents return a copy of an FB_Vec3 with the result.
##### Examples
- Right cross product Vec3 one by Vec3 two and store the result in Vec3 one.<br>
`fbVec1.CrossVec3(fbVec2);`  
- Right cross product Vec3 one by Vec3 two and return a copy of the result. Vec3 one and Vec3 two are unchanged.<br>
`fbVec3 := F_Cross(fbVec1, fbVec2);`  
### Functions
#### F_AxisAngleQuat
- Given a Vec3 representing an axis and an angle in radians, returns an FB_Quaternion representing the rotation about the given axis by the specified angle.
#### F_Cross
- Given two Vec3s, return the cross product formed by Vec3L X Vec3R.
#### F_Dot
- Given two Vec3s, return the dot product.
#### F_EulerRotateVec3Frame
- Given a Vec3, 3 euler angles, and a rotation order, return a new Vec3 that represents the same point but in a frame of reference rotated by the given euler angles.
#### F_EulerRotateVec3Point
- Given a Vec3, 3 euler angles, and a rotation order, return a new Vec3 that represents the given point rotated by the given euler angles.
#### F_EulerToQuat
- Given 3 euler angles, a rotation order, and a boolean to select a Frame rotation or a Point rotation, return the quaternion describing the rotation by the given euler angles.
#### F_MulQuat
- Multiply the first argument quaternion by the second qrgument quaternion on the right. Return a copy of the result. The inputs are unmodified.
#### F_NormalizedQuat
- Return a new FB_Quaternion that represents the normalized version of the input quaternion. The input quaternion is unchanged.
#### F_NormalizedVec3
- Return a new FB_Vec3 that represents the normalized version of the input vector. The input vector is unchanged.
#### F_NormQuat
- Return the norm of the given quaternion.
#### F_NormSqQuat
- Return the norm squared of the given quaternion. Used to limit floating point errors and unecessary square root operations.
#### F_NormSqVec3
- Return the norm (length) squared of the given vector. Used to limit floating point errors and unecessary square root operations.
#### F_NormVec3
- Return the norm (length) of the given vector.
#### F_QuatRotateVec3Frame
- Return the given Vec3 as it would appear if it's frame of reference was rotated by the given quaternion.
#### F_QuatRotateVec3Point
- Return the resulting point if the given Vec3 was was rotated by the given quaternion.
