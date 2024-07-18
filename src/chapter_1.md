# RustViz 2.0: Visualizing Rust's Ownership and Borrowing Principles

### Andrew Mahler

<div class="flex-container vis_block" style="position:relative; margin-left:-75px; margin-right:-75px; display: flex;">
	<object type="image/svg+xml" class="ex1 code_panel" data="ex-assets/vis_code.svg"></object>
	<object type="image/svg+xml" class="ex1 tl_panel" data="ex-assets/vis_timeline.svg" style="width: auto;" onmouseenter="helpers('ex1')"></object>
</div>

<br><br>
<br><br>
<br><br>
<br><br>

### What is RustViz?
<!-- originally written by undergrads a few years back -->
RustViz is an educational tool that generates interactive SVG files depicting ownership and borrowing events from Rust code. 
These visualizations, by detailing the state changes of resource owners, aid in developing understanding about Rust's borrow checker.

<div class="flex-container vis_block" style="position:relative; margin-left:-75px; margin-right:-75px; display: flex;">
	<object type="image/svg+xml" class="ex2 code_panel" data="ex-assets/vis_code1.svg"></object>
	<object type="image/svg+xml" class="ex2 tl_panel" data="ex-assets/vis_timeline1.svg" style="width: auto;" onmouseenter="helpers('ex2')"></object>
</div>

<br><br>
<br><br>
<br><br>
<br><br>
<br><br>
<br><br>
<br><br>
<br><br>
<br><br>
 ![Shy Rustacean](assets/rustacean.png)

### Why Rust?
- Rust is unique in that it achieves memory safety without the need for a garbage collector <!-- 70% or more of all security vulnerabilities are caused by memory safetyissue-->
- It eliminates a whole class of concurrency bugs by how it handles references <!-- Immutable v Mutable -->
- Rust has become extremely popular over the last few years as a low-level systems language <!-- As a replacement for C/C++ -->
- *Why RustViz?:* Rust's Borrow Checker is frequently cited as the most difficult part of learning Rust <!-- Importance of understanding bc fundamentals to write efficient/elegant code -->


<br><br>
<br><br>
<br><br>
<br><br>
<br><br>
<br><br>

### RustViz2.0 vs RustViz
- Visualization generation is now completely automatic 
```
/* --- BEGIN Variable Definitions ---
Owner s; Owner mut x; Owner y; Owner some_string;
Function String::from();
Function takes_ownership();
Function println!()
--- END Variable Definitions --- */
 fn main() {
    let s = String::from("hello"); // !{ Move(String::from()->s) }
    takes_ownership(s); // !{ Move(s->takes_ownership()) }
    let mut x = 5; // !{ Bind(x) }
    let y = x; // !{ Copy(x->y) }
    x = 6; // !{ Bind(x) }
} // !{ GoOutOfScope(s), GoOutOfScope(x), GoOutOfScope(y) }

fn takes_ownership(some_string: String) { // !{ InitOwnerParam(some_string) }
    println!("{}", some_string); // !{ PassByStaticReference(some_string->println!()) }
} // !{ GoOutOfScope(some_string) }
```

- RustViz2.0 supports more language features: 
    - Dereference logic
    - Reference aliasing
    - Conditionals, loops
    - Enums


<br><br>
<br><br>
<br><br>
<br><br>
<br><br>
<br><br>

### Learning from an Example

<div class="flex-container vis_block" style="position:relative; margin-left:-75px; margin-right:-75px; display: flex;">
	<object type="image/svg+xml" class="ex3 code_panel" data="ex-assets/vis_code2.svg"></object>
	<object type="image/svg+xml" class="ex3 tl_panel" data="ex-assets/vis_timeline2.svg" style="width: auto;" onmouseenter="helpers('ex3')"></object>
</div>

<br><br>
<br><br>
<br><br>
<br><br>
<br><br>
<br><br>

### Goals for the Future
1. Expand the support for more language features: 
    - Chained method calls
    - Conditional let bindings (ie `let x = if <expr> {...} else {...};` )
    - Match expressions
    - Lifetimes
2. Detail anonymous owner interactions
3. More sophisticated reference logic <!-- would require dataflow analysis -->
4. Make cool art

<div class="flex-container vis_block" style="position:relative; margin-left:-75px; margin-right:-75px; display: flex;">
	<object type="image/svg+xml" class="ex4 code_panel" data="ex-assets/vis_code3.svg"></object>
	<object type="image/svg+xml" class="ex4 tl_panel" data="ex-assets/vis_timeline3.svg" style="width: auto;" onmouseenter="helpers('ex4')"></object>
</div>