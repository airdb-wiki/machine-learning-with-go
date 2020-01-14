# xx

## 矩阵和向量

如果您花费大量时间学习和应用机器学习，则会看到大量关于矩阵和向量的引用。 实际上，许多机器学习算法都归结为一系列针对矩阵的迭代运算。 什么是矩阵和向量，以及我们如何在Go程序中表示它们？

在大多数情况下，我们将使用github.com/gonum中的包来形成和使用矩阵和向量。 这是一系列专注于数值计算的Go软件包，而且它们一直在变得越来越好。


## 向量

向量是数字的有序集合，以行（从左到右）或列（上和下）排列。 向量中的每个数字称为分量。 例如，这可能是代表我们公司销售的数字的集合，或者可能是代表温度的数字的集合。

当然，使用Go slice表示这些有序的数据集合是很自然的，如下所示

```
// Initialize a "vector" via a slice.
var myvector []float64

// Add a couple of components to the vector.
myvector = append(myvector, 11.0)
myvector = append(myvector, 5.2)

// Output the results to stdout.
fmt.Println(myvector)
```

切片确实是有序集合。 但是，它们并不能真正代表行或列的概念，我们仍然需要在切片之上计算出各种矢量运算。 幸运的是，在向量运算方面，gonum提供了gonum.org/v1/gonum/floats来对float64值的切片和gonum.org/v1/gonum/mat进行运算，该运算符与矩阵一起提供了Vector类型（具有相应的方法）

```
// Create a new vector value.
myvector := mat.NewVector(2, []float64{11.0, 5.2})
```

## 向量运算

如此处所述，使用向量必须使用某些特定于向量/矩阵的操作和规则。 例如，如何将向量相乘？ 我们如何知道两个向量是否相似？ gonum.org/v1/gonum/floats和gonum.org/v1/gonum/mat提供用于矢量/切片操作的内置方法和功能，例如点积，排序和距离。 我们将在这里不介绍所有功能，因为有很多功能，但是我们可以对使用向量的能力有一个大致的了解。 首先，我们可以按照以下方式使用gonum.org/v1/gonum/floats

```
// Initialize a couple of "vectors" represented as slices.
vectorA := []float64{11.0, 5.2, -1.3}
vectorB := []float64{-7.2, 4.2, 5.1}

// Compute the dot product of A and B
// (https://en.wikipedia.org/wiki/Dot_product).
dotProduct := floats.Dot(vectorA, vectorB)
fmt.Printf("The dot product of A and B is: %0.2f\n", dotProduct)

// Scale each element of A by 1.5.
floats.Scale(1.5, vectorA)
fmt.Printf("Scaling A by 1.5 gives: %v\n", vectorA)

// Compute the norm/length of B.
normB := floats.Norm(vectorB, 2)
fmt.Printf("The norm/length of B is: %0.2f\n", normB)
```


我们也可以使用 gonum.org/v1/gonum/mat:

```
// Initialize a couple of "vectors" represented as slices.
vectorA := mat.NewVector(3, []float64{11.0, 5.2, -1.3})
vectorB := mat.NewVector(3, []float64{-7.2, 4.2, 5.1})

// Compute the dot product of A and B
// (https://en.wikipedia.org/wiki/Dot_product).
dotProduct := mat.Dot(vectorA, vectorB)
fmt.Printf("The dot product of A and B is: %0.2f\n", dotProduct)

// Scale each element of A by 1.5.
vectorA.ScaleVec(1.5, vectorA)
fmt.Printf("Scaling A by 1.5 gives: %v\n", vectorA)

// Compute the norm/length of B.
normB := blas64.Nrm2(3, vectorB.RawVector())
fmt.Printf("The norm/length of B is: %0.2f\n", normB)
```

两种情况下的语义相似。 如果您仅使用向量（非矩阵）和/或只需要对的切片进行一些轻量和快速的操作
浮动，那么gonum.org/v1/gonum/floatsis可能是一个不错的选择。 但是，如果您同时使用矩阵和向量，并且/或者想使用更广泛的向量/矩阵功能，则最好使用gonum.org/v1/gonum/mat（以及偶尔引用gonum.org/ v1 / gonum / blas / blas64）。


## 矩阵
矩阵和线性代数对许多人来说似乎很复杂，但是简单地说，矩阵只是数字的矩形组织，线性代数决定了与之相关的规则。 例如，数字A排列在4 x 3矩形上的矩阵A可能看起来像这样

$$\begin{bmatrix}
{a_{11}}&{a_{12}}&{a_{13}}&{a_{14}}\\
{a_{21}}&{a_{22}}&{a_{23}}&{a_{24}}\\
{a_{31}}&{a_{32}}&{a_{23}}&{a_{34}}\\
{a_{41}}&{a_{42}}&{a_{23}}&{a_{44}}\\
\end{bmatrix}$$

A的组成部分（a11，a12等）是我们排列到矩阵中的单个数字，下标表示组成部分在矩阵中的位置。 第一个索引是行索引，第二个索引是列索引。 更一般而言，A可以具有M行和N列的任何形状/大小: 

$$\begin{bmatrix}
{a_{11}}&{a_{12}}&{\cdots}&{a_{1N}}\\
{a_{21}}&{a_{22}}&{\cdots}&{a_{2N}}\\
{\vdots}&{\vdots}&{\ddots}&{\vdots}\\
{a_{M1}}&{a_{M2}}&{\cdots}&{a_{MN}}\\
\end{bmatrix}$$

为了使用gonum.org/v1/gonum/mat形成这样的矩阵，我们需要创建一个切片offloat64值，该值是所有矩阵组件的平面表示。 例如，在我们的示例中，我们要形成以下矩阵:

$$\begin{matrix}
1.2&-5.7\\
-2.4&7.3\\
\end{matrix}$$

我们将需要如下创建一个float64值切片:

```
// Create a flat representation of our matrix.
components := []float64{1.2, -5.7, -2.4, 7.3}
```

然后，我们可以提供此信息以及尺寸信息togonum.org/v1/gonum/mat以形成一个新的mat.Dense矩阵值：

```
// Form our matrix (the first argument is the number of
// rows and the second argument is the number of columns).
a := mat.NewDense(2, 2, data)

// As a sanity check, output the matrix to standard out.
fa := mat.Formatted(a, mat.Prefix(" "))
fmt.Printf("mat = %v\n\n", fa)
```


请注意，我们还在gonum.org/v1/gonum/mat中使用了漂亮的格式化逻辑来打印矩阵以进行完整性检查。 运行此命令时，应该看到以下内容：

```
$ go build
$ ./myprogram
A = [ 1.2 -5.7]
    [-2.4  7.3]
```


然后，我们可以通过内置方法访问和修改A中的某些值：

```
// Get a single value from the matrix.
val := a.At(0, 1)
fmt.Printf("The value of a at (0,1) is: %.2f\n\n", val)

// Get the values in a specific column.
col := mat.Col(nil, 0, a)
fmt.Printf("The values in the 1st column are: %v\n\n", col)

// Get the values in a kspecific row.
row := mat.Row(nil, 1, a)
fmt.Printf("The values in the 2nd row are: %v\n\n", row)

// Modify a single element.
a.Set(0, 1, 11.2)

// Modify an entire row.
a.SetRow(0, []float64{14.3, -4.2})

// Modify an entire column.
a.SetCol(0, []float64{1.7, -0.3})



## 矩阵运算
与向量一样，矩阵也有自己的一组算术规则，以及全部特殊操作集。 与矩阵相关的某些算法的行为与您期望的类似。 但是，在做诸如将矩阵相乘或求逆之类的事情时，您需要特别小心。



方便地，gonum.org/v1/gonum/mat为此算法和许多其他特殊操作提供了一个不错的API。 这是显示一些操作的示例，例如加，乘，除等:

```
// Create two matrices of the same size, a and b.
a := mat.NewDense(3, 3, []float64{1, 2, 3, 0, 4, 5, 0, 0, 6})
b := mat.NewDense(3, 3, []float64{8, 9, 10, 1, 4, 2, 9, 0, 2})

// Create a third matrix of a different size.
c := mat.NewDense(3, 2, []float64{3, 2, 1, 4, 0, 8})

// Add a and b.
d := mat.NewDense(0, 0, nil)
d.Add(a, b)
fd := mat.Formatted(d, mat.Prefix("            "))
fmt.Printf("d = a + b = %0.4v\n\n", fd)

// Multiply a and c.
f := mat.NewDense(0, 0, nil)
f.Mul(a, c)
ff := mat.Formatted(f, mat.Prefix("          "))
fmt.Printf("f = a c = %0.4v\n\n", ff)

// Raising a matrix to a power.
g := mat.NewDense(0, 0, nil)
g.Pow(a, 5)
fg := mat.Formatted(g, mat.Prefix("          "))
fmt.Printf("g = a^5 = %0.4v\n\n", fg)

// Apply a function to each of the elements of a.
h := mat.NewDense(0, 0, nil)
sqrt := func(_, _ int, v float64) float64 { return math.Sqrt(v) }
h.Apply(sqrt, a)
fh := mat.Formatted(h, mat.Prefix("              "))
fmt.Printf("h = sqrt(a) = %0.4v\n\n", fh)
```


特别要注意上面的Apply（）方法。 此功能非常有用，因为它允许您将任何功能应用于矩阵的元素。 您可以将相同的函数应用于所有元素，或者使函数依赖于矩阵元素的索引。 例如，您可以使用此方法执行逐个元素
乘法，用户定义功能的应用或第三方程序包中的功能的应用。


然后，对于所有事物，例如行列式，特征值/向量解算器和逆函数，gonum.org / v1 / gonum / mathas都已介绍。 同样，我不会扩展所有功能，但是这里是一些操作的示例：
```
// Create a new matrix a.
a := mat.NewDense(3, 3, []float64{1, 2, 3, 0, 4, 5, 0, 0, 6}) 

// Compute and output the transpose of the matrix.
ft := mat.Formatted(a.T(), mat.Prefix(" "))
fmt.Printf("a^T = %v\n\n", ft)

// Compute and output the determinant of a.
deta := mat.Det(a)
fmt.Printf("det(a) = %.2f\n\n", deta)

// Compute and output the inverse of a.
aInverse := mat.NewDense(0, 0, nil)
if err := aInverse.Inverse(a); err != nil {
    log.Fatal(err)
}

fi := mat.Formatted(aInverse, mat.Prefix(" "))
fmt.Printf("a^-1 = %v\n\n", fi)
```


请注意，在此示例中，当我们需要确保保持完整性和可读性时，我们利用Go的显式错误处理功能。 矩阵并不总是有逆的。 处理矩阵和大型数据集时，会出现各种情况，我们希望确保我们的应用程序符合预期。


