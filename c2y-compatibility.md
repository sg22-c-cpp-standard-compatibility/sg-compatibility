# C2y Compatibility

This file documents the efforts of making C++ compatible with C2y.
That is, with the next version of the C standard after C23.
Find below a table of all papers that have been merged into the C2y working draft,
as well as the C++ compatibility status.

> [!WARNING]
> This table is not yet complete.
> Empty cells will be filled over time,
> and tracking issues will be opened where necessary.

<table>
  <tr>
    <th>WG14 Paper</th>
    <th>WG21 Paper/Issue</th>
    <th>Status</th>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3192.pdf">N3192</a>
      Sequential hexdigits
    </td>
    <td>D4039</td>
    <td>
      <a href="https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues/54">#54</a>
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3064.pdf">N3064</a>
      Writing to multibyte character files
    </td>
    <td></td>
    <td>C wording</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3232.pdf">N3232</a>
      Round-trip rounding
    </td>
    <td></td>
    <td>C wording</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3233.pdf">N3233</a>
      Recommendation for <code>printf</code> rounding
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3239.htm">N3239</a>
      Some constants are literally literals, v2
    </td>
    <td></td>
    <td>C wording</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3242.pdf">N3242</a>
      Problematic use of &quot;correctly rounded&quot;
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3244.pdf">N3244</a>
      Slay Some Earthly Demons I
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3247.pdf">N3247</a>
      <code>fopen</code> <code>&quot;p&quot;</code> and bring <code>fopen</code>'s mode closer to POSIX 202x
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3254.pdf">N3254</a>
      Accessing byte arrays, v4
    </td>
    <td></td>
    <td>
      <a href="https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues/66">#66</a>
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3259.pdf">N3259</a>
      Support <code>++</code> and <code>--</code> on complex values
    </td>
    <td></td>
    <td>
      <a href="https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues/62">#62</a>
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3260.pdf">N3260</a>
      <code>_Generic</code> selection expression with a type operand
    </td>
    <td></td>
    <td>Not relevant</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3273.pdf">N3273</a>
      <code>alignof</code> of an incomplete array type
    </td>
    <td></td>
    <td>✅ C++98</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3274.pdf">N3274</a>
      Remove imaginary types, v3
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3272.htm">N3272</a>
      <code>strftime</code> broken-down structure usage (Option 1: Undefined Behavior)
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3286.pdf">N3286</a>
      Floating-point exception for Macro Replacements
    </td>
    <td></td>
    <td>C wording</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3287.pdf">N3287</a>
      Nonsensical Parenthetical in Mathematics Specification
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3291.pdf">N3291</a>
      Decimal Floating-Point Number Term Misuse
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3298.htm">N3298</a>
      Introduce Complex Literals
    </td>
    <td></td>
    <td>✅ C++98</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3303.pdf">N3303</a>
      <code>HUGE_VAL</code> Corrections
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3305.pdf">N3305</a>
      Leftover <code>WANT_...</code> Macros for &lt;math.h&gt; and Decimal Floating-Point
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3312.pdf">N3312</a>
      Relax Atomic Alignment Requirements
    </td>
    <td></td>
    <td>
      <a href="https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues/42">#42</a>
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3322.pdf">N3322</a>
      Allow Zero Length operations on Null Pointers (Including in the Library)
    </td>
    <td></td>
    <td>✅ C++98</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3323.pdf">N3323</a>
      How Do You Add One To Something? (By Using The Proper Type)
    </td>
    <td></td>
    <td>C wording</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3324.pdf">N3324</a>
      &quot;pole-error&quot; C wording
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3326.pdf">N3326</a>
      Standardize <code>strnlen</code> and <code>wcsnlen</code>
    </td>
    <td></td>
    <td>
      <a href="https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues/63">#63</a>
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3340.pdf">N3340</a>
      Slay Some Earthly Demons II
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3341.pdf">N3341</a>
      Slay Some Earthly Demons III
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3342.pdf">N3342</a>
      Slay Some Earthly Demons IV
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3344.pdf">N3344</a>
      Slay Some Earthly Demons VI
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3345.pdf">N3345</a>
      Slay Some Earthly Demons VII
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3346.pdf">N3346</a>
      Slay Some Earthly Demons VIII
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3349.pdf">N3349</a>
      <code>abs</code> Without Undefined Behavior
    </td>
    <td></td>
    <td>
      <a href="https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues/56">#56</a>
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3353.htm">N3353</a>
      Obsolete Octal and Provide New, Proper Escape Sequences
    </td>
    <td>
        <a href="https://github.com/cplusplus/papers/issues/2055">P0085</a>
        <code>Oo...</code> adding a coherent character sequence to begin octal-literals
    </td>
    <td>
      <a href="https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues/40">#40</a>
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3355.htm">N3355</a>
      Named/Labeled Loops
    </td>
    <td>
      <a href="https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues/41?issue=cplusplus%7Cpapers%7C2212">P3568</a>
      <code>break label;</code> and <code>continue label;</code>
    </td>
    <td>
      <a href="https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues/41">#41</a>
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3356.htm">N3356</a>
      <code>if</code> Declarations
    </td>
    <td></td>
    <td>✅ C++98</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3364.pdf">N3364</a>
      SNAN Initialization
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3366.htm">N3366</a>
      Restartable Functions for Efficient Character Conversions
    </td>
    <td></td>
    <td>
      <a href="https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues/64">#64</a>
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3367.htm">N3367</a>
      More Modern Bit Utilities
    </td>
    <td></td>
    <td>
      <a href="https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues/59">#59</a>
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3369.pdf">N3369</a>
      The <code>_Lengthof</code> Operator
    </td>
    <td></td>
    <td>
      <a href="https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues/61">#61</a>
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3370.htm">N3370</a>
      Case Ranges in <code>switch</code> Statements
    </td>
    <td>
      <a href="https://github.com/cplusplus/papers/issues/2697">P4040</a>
      Case ranges
    </td>
    <td>
      <a href="https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues/52">#52</a>
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3461.pdf">N3461</a>
      range error definition followup
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3363.pdf">N3363</a>
      <code>&lt;stdarg.h&gt;</code> Wording
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3401.htm">N3401</a>
      SIGFPE and I/O (v2)
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3405.pdf">N3405</a>
      Improved Wording for Treatment of Error Conditions in <code>&lt;math.h&gt;</code>
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3409.pdf">N3409</a>
      Slay Some Earthly Demons X
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3410.pdf">N3410</a>
      Slay Some Earthly Demons XI
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3411.pdf">N3411</a>
      Slay Some Earthly Demons XII
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3418.pdf">N3418</a>
      Slay Some Earthly Demons XIV
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3447.htm">N3447</a>
      Chasing Ghost I - Constant Expressions
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3448.htm">N3448</a>
      Chasing Ghosts II - Accessing Allocated Storage
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3451.pdf">N3451</a>
      Initialization of Anonymous Structures and Unions (v2)
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3452.pdf">N3452</a>
      Complex Literals Warning
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3459.pdf">N3459</a>
      Integer and Arithmetic Constant Expressions
    </td>
    <td></td>
    <td>C wording</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3460.pdf">N3460</a>
      Complex Operators
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3466.pdf">N3466</a>
      Clarifications on Null Pointers in the Library
    </td>
    <td></td>
    <td>C wording</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3469.htm">N3469</a>
      Big Array Size Survey
    </td>
    <td></td>
    <td><a href="https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues/61">#61</a></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3478.pdf">N3478</a>
      Slay Some Earthly Demons XIII
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3481.pdf">N3481</a>
      Slay Some Earthly Demons XVI
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3482.pdf">N3482</a>
      Slay Some Earthly Demons XVII
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3492.pdf">N3492</a>
      Improved treatment of error conditions for functions that round result
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3496.htm">N3496</a>
      Clarify the Specification of the Width Macros
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3505.pdf">N3505</a>
      Preprocessor integer expressions, II
    </td>
    <td></td>
    <td>
      <a href="https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues/60">#60</a>
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3347.pdf">N3347</a>
      Slay Some Earthly Demons IX
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3348.pdf">N3348</a>
      Matching of Multi-Dimensional Arrays in Generic Selection Expressions
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3457.htm">N3457</a>
      The <code>__COUNTER__</code> predefined macro
    </td>
    <td>
        <a href="https://github.com/cplusplus/papers/issues/2041">P3384</a>
        <code>__COUNTER__</code>
    </td>
    <td>
        <a href="https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues/49">#49</a>
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3484.pdf">N3484</a>
      Slay Some Earthly Demons V
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3500.pdf">N3500</a>
      Clarification for Complex Suffix Specification
    </td>
    <td></td>
    <td>C wording</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3511.pdf">N3511</a>
      Remove &quot;category&quot; from &quot;type category&quot; in footnote
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3517.htm">N3517</a>
      Array subscripting without decay
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3525.htm">N3525</a>
      <code>static_assert</code> without UB
    </td>
    <td></td>
    <td>C wording</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3532.pdf">N3532</a>
      Member Access of an Incomplete struct Should Not Be Allowed
    </td>
    <td></td>
    <td>C wording</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3535.pdf">N3535</a>
      <code>frexp</code> and double-double
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3536.pdf">N3536</a>
      Clarify wording of <code>cproj</code>
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3537.pdf">N3537</a>
      Correct and clarify 7.3.1 Introduction of Complex Arithmetic <code>&lt;complex.h&gt;</code>
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3544.txt">N3544</a>
      Classification of the register Storage-class Specifier
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3558.htm">N3558</a>
      Chasing Ghosts I: Constant Expressions and Objects of Known Constant Size
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3563.pdf">N3563</a>
      Representation of Pointers and <code>nullptr_t</code>
    </td>
    <td>
      <a href="https://wg21.link/CWG2966">CWG2966</a>
      Alignment and value representation of <code>std::nullptr_t</code>
    </td>
    <td>✅ C++26</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3577.txt">N3577</a>
      Rename <code>uimaxabs</code> to <code>umaxabs</code>
    </td>
    <td></td>
    <td>
      <a href="https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues/56">#56</a>
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3598.pdf">N3598</a>
      Make text consistent between <code>creal</code> and <code>cimag</code>
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3607.htm">N3607</a>
      Retire the Concept of Consume Operations
    </td>
    <td>
        <a href="https://github.com/cplusplus/papers/issues/2129">P3475</a>
        Defang and deprecate <code>memory_order::consume</code>
    </td>
    <td>✅ C++26</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3623.pdf">N3623</a>
      Slay Some Earthly Demons XIV: Definition of Main
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3652.pdf">N3652</a>
      Composite types v1.3
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3622.txt">N3622</a>
      Allowing calling <code>static inline</code> within <code>extern inline</code>
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3715.pdf">N3715</a>
      Static assertions in expressions, v2.2
    </td>
    <td></td>
    <td>
      <a href="https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues/65">#65</a>
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3646.pdf">N3646</a>
      Clarification of range error condition for <code>atan2</code>
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3647.pdf">N3647</a>
      Semantic rules for constant evaluation
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3648.pdf">N3648</a>
      Improved language for return type vs. return value
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3653.pdf">N3653</a>
      Earthly Demon: Accessing a Member of an Atomic Structure or Union
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3655.pdf">N3655</a>
      Make implicit undefined behavior in <code>mtx_destroy()</code> explicit, Mutex Option 2
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3773.htm">N3773</a>
      C23 Issues Resolution
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3747.pdf">N3747</a>
      Integer Sets, v5
    </td>
    <td>
      <a href="https://github.com/cplusplus/papers/issues/2420">P3666</a>
      Bit-precise integers
    </td>
    <td>
      <a href="https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues/57">#57</a>
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3751.txt">N3751</a>
      Refector Syntax of Preprocessing Directives
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3755.txt">N3755</a>
      Refactor order of memory functions
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3786.htm">N3786</a>
      Remove Imaginary I, v3
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3788.htm">N3788</a>
      Clean up atomics, non-normative changes, v7
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3833.htm">N3833</a>
      Integer Constant Expression-Initialized <code>const</code> Integer-Typed Declarations are Implicitly <code>constexpr</code>, r4
    </td>
    <td></td>
    <td>✅ C++11</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3700.pdf">N3700</a>
      Wording Improvement: Generation of Non-Value Representation
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3703.pdf">N3703</a>
      Preferred Quantum Exponent
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3704.pdf">N3704</a>
      Clean up <code>frexp</code>, <code>ldexp</code>, <code>scalbn</code>
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3705.htm">N3705</a>
      Bit-Precise enum
    </td>
    <td>
      <a href="https://github.com/cplusplus/papers/issues/2420">P3666</a>
      Bit-precise integers
    </td>
    <td>
      <a href="https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues/57">#57</a>
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3714.pdf">N3714</a>
      Busting Another Ghost: UB#11: Value of <code>auto</code> Object
    </td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3722.pdf">N3722</a>
      Generic Replacement and Immediate Constants
    </td>
    <td></td>
    <td>Not relevant</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3731.pdf">N3731</a>
      Range Bounds for Math Functions
    </td>
    <td></td>
    <td>C wording</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3732.pdf">N3732</a>
      Floating Expression Evaluated in Translation
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3737.pdf">N3737</a>
      Refine the Language of Error Reporting
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3738.pdf">N3738</a>
      Preferred Quantum Exponent for <code>nextafterN</code>
    </td>
    <td></td>
    <td>C wording</td>
  </tr>
  <tr>
    <td>
      <a href="https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3756.txt">N3756</a>
      Ignite Annex I (Replace it with an &quot;Unused&quot; Annex)
    </td>
    <td></td>
    <td>Editorial</td>
  </tr>
</table>

Explanation for the *Status* column:

<dl>
  <dt>✅ C++</dt>
  <dd>Change is compatible with C++.</dd>
  <dt>#NN</dt>
  <dd>See the tracking issue for status.</dd>
  <dt>C wording</dt>
  <dd>
    Change to C wording (usually a fix).
    This status only applies if the C wording is also automatically inherited by C++
    or only necessary in the C wording.
    Normative defects that need action in C++ should not have this status.
  </dd>
  <dt>Not relevant</dt>
  <dd>
    Won't be ported to C++, such as anything relating to <code>_Generic</code>.
  </dd>
  <dt>Editorial</dt>
  <dd>
    Editorial changes to the C standard.
    Either not relevant to C++ or automatically inherited.
  </dd>
</dl>
