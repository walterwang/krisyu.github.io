---
layout: post
title: "Apple simd/swift 来算矩阵 matrix"
---

# Apple simd 来算矩阵 matrix

keywords： Swift, simd, vector, matrix, matrix multiply matrix, matrix multiply vector ...

警告，一篇由API堆砌的..

### 向量  vector 

#### vector3 vs float3 vs vector_float3 vs Float32


厉害了我的 Swift，看一个项目做一个东西，居然有这么多...然而看一看API， 我应该选 float3 而非 vector\_float3, 因为OC对应 vect\_float3 , c++ 对应 simd::float3， 至少它遵守 CustomDebugStringConvertible 协议，更容易打印

而vector3 是用来 init的， 默认生成的是 vector\_double3，而 vector\_double3 是 double3 的另一个名字, 就像 vector\_float3 是 float3的另一个名字一样



```
public typealias vector_float3 = float3
```


```
public func vector3(_ __x: Double, _ __y: Double, _ __z: Double) -> vector_double3

public typealias vector_double3 = double3
```


然而Float32 根本就是精度确定的Float. 跟别的不是同一样东西。


看一下 float3 的完整API

```
/// A vector of three `Float`.  This corresponds to the C and
/// Obj-C type `vector_float3` and the C++ type `simd::float3`.
public struct float3 : ExpressibleByArrayLiteral, CustomDebugStringConvertible {

    public var x: Float

    public var y: Float

    public var z: Float

    /// Initialize to the zero vector.
    public init()

    /// Initialize a vector with the specified elements.
    public init(_ x: Float, _ y: Float, _ z: Float)

    /// Initialize a vector with the specified elements.
    public init(x: Float, y: Float, z: Float)

    /// Initialize to a vector with all elements equal to `scalar`.
    public init(_ scalar: Float)

    /// Initialize to a vector with elements taken from `array`.
    ///
    /// - Precondition: `array` must have exactly three elements.
    public init(_ array: [Float])

    /// Initialize using `arrayLiteral`.
    ///
    /// - Precondition: the array literal must exactly three elements.
    public init(arrayLiteral elements: Float...)

    /// Access individual elements of the vector via subscript.
    public subscript(index: Int) -> Float

    /// Debug string representation
    public var debugDescription: String { get }
}

```

#### 点乘 * 

首先要明了一个东西，就是默认的 vector3 和 float3 是不能结合的！ 它们是不会幸福的。

Swift 会报错。

```
import simd

let v3 = vector3(3.0, 2.0 , 1.0)
let f3 = float3(3.0, 2.0, 1.0)
```

如果我非常强制/强势的测试


```
float3(Float(v3.x), Float(v3.y), Float(v3.z)) * f3

```

但是如果使用 let v3 = vector_float3(3.0, 2.0 , 1.0) 则可以通过，但是why 作，都使用 float3 好了

#### 叉乘 cross(v1, v2)

叉乘这样算


```

let u = float3(1, 0, 0)
let v = float3(0, 1, 0)

print(cross(u, v))
// float3(0.0, 0.0, 1.0)
```

#### 别的

别的就直接用 + - * 就可以完成了

```
print(u + v)
print(u - v)
print(u * 3)
```


### 矩阵 matrix

再一次感慨， 因为发现有人用 matrix_float4x4， 有人用 float4x4

#### matrix_float4x4 vs float4x4

matrix_float4x4 用列的方式存储的， 更多是为了通用性能存在。

>  For compatibility with common graphics libraries, these matrices are stored in column-major order, and implemented as arrays of column vectors.


还发现了

> vectors of length three are internally represented as length four vectors with one element of padding (for alignment purposes).  This means that when a floatNx3 or doubleNx3 is viewed as a vector, it appears to have 4\*N elements instead of the expected 3\*N (with one padding element at the end of each column).  The matrix elements are laid out in memory as follows:  { 0, 1, 2, x, 3, 4, 5, x, ... }

看它的API

```
public struct matrix_float4x4 {

    public var columns: (vector_float4, vector_float4, vector_float4, vector_float4)

    public init()

    public init(columns: (vector_float4, vector_float4, vector_float4, vector_float4))
}
```


而如果整个项目都是在 swift 中完成的话，那么应该 vote for float4x4,它遵守 CustomDebugStringConvertible 协议， 而且它有更多的方法，看它的API


它也可以直接用 matrix\_float4x4 来init， float4x4也可以直接获得matrix\_float4x4

但是我感觉还是受到了伤害，这个默认的init 还是列优先的init，虽然我们可以写 float4x4.init(rows:~~)，但是默认 init 还是列优先，并且subscript获得的也是列

好气哦（是因为已经用过glm的原因么， 但是所以其实注意一点也不会出错么（怀疑自我ing


> Matrix-Vector multiplication.  Keep in mind that matrix types are named `FloatNxM` where `N` is the number of *columns* and `M` is the number of *rows*, so we multiply a `Float3x2 * Float3` to get a `Float2`, for example.





```
public struct float4x4 : CustomDebugStringConvertible {

    /// Initialize matrix to zero.
    public init()

    /// Initialize matrix to have `scalar` on main diagonal, zeros elsewhere.
    public init(_ scalar: Float)

    /// Initialize matrix to have specified `diagonal`, and zeros elsewhere.
    public init(diagonal: float4)

    /// Initialize matrix to have specified `columns`.
    public init(_ columns: [float4])

    /// Initialize matrix to have specified `rows`.
    public init(rows: [float4])

    /// Initialize matrix from corresponding C matrix type.
    public init(_ cmatrix: matrix_float4x4)

    /// Get the matrix as the corresponding C matrix type.
    public var cmatrix: matrix_float4x4 { get }

    /// Access to individual columns.
    public subscript(column: Int) -> float4

    /// Access to individual elements.
    public subscript(column: Int, row: Int) -> Float

    /// A textual representation of this instance, suitable for debugging.
    public var debugDescription: String { get }

    /// Transpose of the matrix.
    public var transpose: float4x4 { get }

    /// Inverse of the matrix if it exists, otherwise the contents of the
    /// resulting matrix are undefined.
    public var inverse: float4x4 { get }
}
```

#### 矩阵相乘

如果用的 matrix_float4x4, 用

```
 public func matrix_multiply(_ __x: matrix_float4x4, _ __y: matrix_float4x4) -> matrix_float4x4
```

如果是 float4x4 ，直接用 * 就可以


#### 矩阵和向量之间的运算

之前矩阵已经notes过关于维度的问题，所以如果要想实现平移

```
[1	0	0  10]		[10]    [ 20 ]
[0	1	0	0]  * 	[10] =  [ 10 ]
[0	0	1	0]		[10] 	 [ 10 ]
[0	0	0	1]		[1]     [ 1]
```


模拟以上运算 ↑

```
var m5 = float4x4(1)
m5[3][0] = 10

print(m5)
// float4x4([[1.0, 0.0, 0.0, 0.0], [0.0, 1.0, 0.0, 0.0], [0.0, 0.0, 1.0, 0.0], [10.0, 0.0, 0.0, 1.0]]) 
// print 也是用列表示的

print(m5 * float4(10,10,10,1)) 正确
// float4(20.0, 10.0, 10.0, 1.0)

print(float4(10,10,10,1) * m5)
// float4(10.0, 10.0, 10.0, 101.0) 侬在做啥，错误 🙅
```




