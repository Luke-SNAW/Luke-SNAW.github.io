
> https://jsdev.space/js-garbage-collection/

In JavaScript, memory management is vital for both performance and stability. The garbage collection (GC) mechanism handles automatic memory reclamation, but there are several algorithms employed to manage this efficiently. Below is an in-depth exploration of the three classic GC algorithms:

## 1. In-depth Analysis of Three Garbage Collection Algorithms

### Mark-and-Sweep Algorithm

**Core Principle**: Identify surviving objects through reachability analysis. Process:

- **Marking**: Start from GC roots, such as global objects and active function call stacks.
- **Tracking**: Perform depth-first traversal to find all reachable objects.
- **Cleanup**: Reclaim memory from unmarked objects.

```js
function markAndSweep() {
  // Mark phase
  let worklist = [...roots]
  while (worklist.length > 0) {
    const obj = worklist.pop()
    if (!obj.marked) {
      obj.marked = true
      worklist.push(...obj.references)
    }
  }

  // Sweep phase
  for (const obj of heap) {
    if (!obj.marked) {
      freeMemory(obj)
    } else {
      obj.marked = false // Reset marking
    }
  }
}
```

**Advantages:**

- Solves the circular reference problem.
- Efficient with large-scale memory management.
- High memory utilization.

**Disadvantages:**

- Memory fragmentation (though this can be optimized with mark-defragmentation).
- Full heap scan can cause Stop-the-World (STW) pauses.

### Reference Counting

**Core Principle**: Track object lifecycle using a reference counter.

```js
class RefCountedObject {
  constructor() {
    this.count = 1 // Initial reference count
    this.references = new Set()
  }

  addRef() {
    this.count++
  }

  release() {
    if (--this.count === 0) {
      this._destroy()
    }
  }

  _destroy() {
    this.references.forEach((obj) => obj.release())
    freeMemory(this)
  }
}
```

**Pitfall:**

- **Circular Reference Issue**: Objects that reference each other can never reach zero count, causing a memory leak.

```js
function createCycle() {
  let objA = new RefCountedObject()
  let objB = new RefCountedObject()

  objA.ref = objB // objB.count = 2
  objB.ref = objA // objA.count = 2
}

createCycle()
// After execution: objA.count = 1, objB.count = 1 → Memory leak
```

**Modern Usage:**

- Used in specialized cases (e.g., COM components).
- Forms the basis for APIs like `WeakRef`. read also [Master JavaScript WeakRef & FinalizationRegistry](https://jsdev.space/memory-management-js/)
- Often combined with mark-and-sweep for better efficiency.

### Generational Garbage Collection

**Core Principle**: The Weak Generation Hypothesis suggests younger objects tend to die faster. **V8 Specific Implementation**: Objects that survive several GC cycles in the "new generation" are promoted to the "old generation."

```js
// Example: New Space Memory Layout (Semispace)
class NewSpace {
  constructor() {
    this.fromSpace = new ArrayBuffer(4 * 1024 * 1024) // 4MB
    this.toSpace = new ArrayBuffer(4 * 1024 * 1024)
    this.allocPtr = 0
  }

  allocate(size) {
    if (this.allocPtr + size > this.fromSpace.byteLength) {
      this.doScavenge()
    }
    const ptr = this.allocPtr
    this.allocPtr += size
    return ptr
  }

  doScavenge() {
    // Cheney's Algorithm to copy live objects
    let scanPtr = 0
    this.allocPtr = 0

    while (scanPtr < this.allocPtr) {
      const obj = this.toSpace[scanPtr]
      for (const ref of obj.references) {
        if (ref.isInFromSpace()) {
          copyToNewSpace(ref)
        }
      }
      scanPtr += obj.size
    }
    ;[this.fromSpace, this.toSpace] = [this.toSpace, this.fromSpace]
  }
}
```

### Comparison of generational strategies:

| **Generation**   | **Proportion** | **GC Frequency** | **Algorithm**         | **Optimization Target** |
| ---------------- | -------------- | ---------------- | --------------------- | ----------------------- |
| Young Generation | 5%             | High frequency   | Scavenge              | Throughput              |
| Old Generation   | 95%            | Low frequency    | Mark-sweep/collection | Latency control         |

## 2. Evolution of Modern GC Algorithms

### New Generation Scavenge Algorithm

The Cheney algorithm facilitates fast recycling by alternating between "From" and "To" spaces:

```js
function scavenge() {
  let from = currentNewSpace
  let to = newNewSpace

  for (let obj of reachableObjects) {
    copyObject(obj, to)
    forwardPointer(obj, to)
  }

  swapSpaces(from, to)
}
```

### Old Generation Mark-Sweep Optimization

V8 optimizes the old generation using a three-color marking method combined with incremental marking to avoid long STW pauses:

- **White**: Unvisited objects
- **Gray**: Objects being accessed
- **Black**: Objects already visited

```js
function incrementalMarking() {
  let worklist = getGreyObjects()

  while (worklist.length > 0 && !shouldYield()) {
    const obj = worklist.pop()
    markObject(obj)
    for (const ref of getReferences(obj)) {
      if (!isMarked(ref)) {
        markGrey(ref)
        worklist.push(ref)
      }
    }
  }

  if (worklist.length > 0) {
    requestIdleCallback(incrementalMarking)
  }
}
```

## 3. Modern Forms of Memory Leaks

### Closure Trap

```js
function createClosureLeak() {
  const hugeData = new Array(1e6).fill("*")
  return function () {
    // Closure inadvertently holds onto hugeData
    console.log("Closure executed")
  }
}

let leakedClosure = createClosureLeak()
```

### Reference Relics in Modern Frameworks (React Example)

```jsx
function Component() {
  const [data, setData] = useState(null)

  useEffect(() => {
    const timer = setInterval(() => {
      fetchData().then((result) => {
        setData(result) // May hold old references if missing dependencies
      })
    }, 1000)

    return () => clearInterval(timer)
  }, []) // Missing dependency could cause memory leaks
}
```

## 4. GC Performance Optimization Strategies

### Object Pooling

By reusing memory through object pools, you can minimize the need for frequent garbage collection.

```js
class VectorPool {
  constructor() {
    this.pool = []
  }

  create(x, y) {
    return this.pool.pop() || { x, y }
  }

  release(vec) {
    vec.x = null
    vec.y = null
    this.pool.push(vec)
  }
}

// Usage example
const pool = new VectorPool()
const v1 = pool.create(10, 20)
// After usage
pool.release(v1)
```

### Optimizing Memory Access Patterns

Improving memory access patterns can lead to better cache utilization, reducing the performance impact of GC.

```js
// Inefficient access pattern
function processMatrix(matrix) {
  for (let col = 0; col < 1000; col++) {
    for (let row = 0; row < 1000; row++) {
      process(matrix[row][col]) // Breaks memory locality
    }
  }
}

// Optimized access pattern
function optimizedProcess(matrix) {
  for (let row = 0; row < 1000; row++) {
    const rowData = matrix[row]
    for (let col = 0; col < 1000; col++) {
      process(rowData[col]) // Sequential access
    }
  }
}
```

## Conclusion

Garbage collection in JavaScript plays a critical role in optimizing both memory and performance. While automatic GC can help prevent memory leaks, understanding its mechanisms and strategically optimizing your code can lead to significant performance gains. The balance between automatic and manual memory management is key to developing high-performance web applications.
