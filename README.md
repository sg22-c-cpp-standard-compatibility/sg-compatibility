
# SG22 Compatibility

Welcome to the SG22 C & C++ Compatibility Repository. Here you will find meeting minutes, presentations, notes, documentation, and tracking for various compatibility issues between C and C++.

Go through the [issues list here](https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues) if you want to see if there is a compatibility issue that is open for something you care about. Look at the [closed issues list](https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues?q=is%3Aissue+is%3Aclosed) to see if this is something that has already been addressed.

# Chairs

- Nina Dinka Ranns (primarily Working Group 21 - C++)
- Davis Herring (primarily Working Group 21 - C++, co-chair)
- [JeanHeyd Meneide (primarily Working Group 14 - C)](mailto:wg14@soasis.org)

Feel free to contact us when necessary.


# Useful Reading

- For a good, high-level overview of C and C++ compatibility issues and (intentional) divergence, see Aaron Ballman's excellent [P2735 - C XOR C++](https://wg21.link/p2735r0).


# SG22 2024 Meeting Summaries

This document contains summaries of SG22 meetings held during 2024.

- [January 31st, 2025](#January-31st-2025) - P2746, P2142, and P3248
- [January 7th, 2025](#January-7th-2025) - P3477R0, P3475R0, and P3384R0
- [August 28th, 2024](#August-28th-2024) - P3309 and P3140
- [July 26th, 2024](#July-26th-2024) - P2865 and P2866
- [February 1st, 2024](#February-1st-2024) - Provenance and Memory Model Discussion

# January 31st, 2025
## Agenda

- [P2746 Deprecate and Replace Fenv Rounding Modes (Hans Boehm)](https://github.com/cplusplus/papers/issues/1437)
- [P3248 Require [u]intptr_t (Gonzalo Brito Gadeschi)](https://github.com/cplusplus/papers/issues/1909)
- [P2142 Allow '.' operator to work on pointers (Jim Buckeyne)](https://github.com/cplusplus/papers/issues/868)

## Attendees
NR      Nina Ranns (chair)

DH      Davis Herring (co-chair, scribe)

HB      Hans Boehm

JG      Jens Gustedt

JC      Joshua Cranmer

CJ      Corentin Jabot

AB      Aaron Ballman

JB      Jim Buckeyne

RB      Rajan Bhakta

KE      Khalil Estell

GB      Gonzalo Brito

VV      Ville Voutilainen

SV      Steven Vormwald

LV      Lauri Vasama

LY      Li Yihe

AM      Alisdair Meredith

PM      Paul McKenney

JM      Jens Maurer

PP      Paul Preney

JS      Jan Schultke

NL      Nevin Liber

## Meeting Summary


### P2746 Deprecate and Replace Fenv Rounding Modes


(HB presents slides for P2746.)

HB: Most people don't know `#pragma STDC FENV_ACCESS` is even a feature, and it's not been well supported in C++.

HB: SG6 tried to find use cases and found 3, none of which seems compelling:

HB: Interval arithmetic might be better implemented in assembly anyway.

HB: WG14 mentioned using rounding modes for fuzz testing, but it's heuristic at best.

HB: `rint` having the rounding mode as an implicit argument is a misfeature.

HB: IEEE is moving in the direction of static rounding modes, but that may not be enough.

HB: I don't agree with IEEE/WG14 that rounding modes should be bound to a scope or time interval at all, since computing an upper bound is not the same as rounding every subexpression upward.

JG: (about a slide) There was no C20; before C23 is C17.

HB: A member function tells whether results are correctly rounded.

DH: The ODR might not account for different rounding in different TUs.

HB: Guy Davidson wants reproducible operators, which could be a wrapper for the correctly-rounded non-operator operations.

HB: I consider `#pragma STDC FENV_ROUND`'s block-based nature a disadvantage.

RB: We did consider `constexpr` interactions in C in adding `FENV_ROUND`.

HB: It seems that language divergence here has been deemed acceptable.

RB: Changing constexpr rounding would happen only on new C23 request.

HB: We can look at the library proposal, but that's probably less interesting here.

NR: I'd like to hear what WG14 thinks will happen if C++ deprecates these functions.

JG: I'm not opposed to removing the dynamic environment support.  I don't like encapsulating the rounding mode into a type, since we don't want many such types in C and selecting among them requires expertise.

HB: Maybe I should show the proposed interface.

(HB presents P2746 itself.)

HB: This proposal is C++-centric: it doesn't introduce new floating-point types that have a rounding mode, just introduce a class type that holds one and uses it for each operation.  The syntactic convenience works well in C++, but is not C-friendly.

HB: (in response to a scribing clarification) Davis was actually the one who suggested this interface.

JC: I'm working on floating-point semantics in C++; the dynamic environment in general is a problem for both languages.  The interaction with compile-time features for rounding like template parameters is complicated.

HB: Matthias has brought this up repeatedly, but it's very hard to specify what implementations actually do here.  Floating-point exceptions are an interesting problem, but SG6 decided to defer them.  Flush-to-zero is hard to specify.

JM: Why do we believe the static `#pragma` is bad (other than syntactically)?  It seems implementable.

JC: Inline functions would want to inherit the `#pragma` but can't (you can't have it as a template argument).

JS: Even in C you could call a real function.

JC: Which is the common case in C++.

RB: User-defined functions don't use the ambient static rounding mode.

HB: The C23 rules do affect the standard functions.

RB: Because they are the IEEE functions.

HB: I prefer the per-operation specification because except in special cases you need to consider each operation separately.

JS: Is there an example where you want it per-operation, not per type?

HB: Use cases are rare, but you can't implement interval arithmetic with a fixed rounding mode.

NR: Going back to WG14/WG21 compatibility, do I understand correctly that we already have an incompatibility with C23 that we can't remove?

RB: C++ doesn't specify it, but it could.

DH: Would the effects on the standard library functions of the C23 feature be implementable/desirable in C++?

RB: I think it's desirable, given the IEEE correspondence.

JG: How widely implemented are the C pragmas?

RB: C99 pragmas are often accepted and ignored.

JC: Clang implements them; NVCC doesn't support `FENV_ACCESS`, but a similar per-function feature; GCC has only command-line flags.

RB: They all do have flags.

JC: C23 pragmas are partially implemented in Clang, without the library-function support.

HB: So constant evaluation follows the rounding mode.

JC: Yes.

NR: I don't think we can do any polls here; this needs to be seen by SG6 again at least.

HB: This has been approved by SG6, but I'd like them to see it again.

NR: Davis, are you considering writing a WG21 paper on the C23 feature?

DH: No; I was trying to understand how durable the existing incompatibility is.


### P3248 Require [u]intptr_t

(GB presents slides for P3248R2.)

GB: I'm asking WG14 whether there is some other impact we didn't consider.

DH: It's true that "pointer value" and "address" are different, but `uintptr_t` still can't hold a pointer value; it might be a third thing, but the platforms with such a third thing (like CHERI) aren't conforming anyway, so it might not matter.

GB: The intent is just that it have C's semantics.

JG: I proposed this for C23, but it wasn't adopted.  I see in `<cstdint>` that C++ isn't based on C23 which bases everything on widths.

NR: That's in progress.

JM: There's a paper, but I don't know whether it addresses that particular point.  This paper is like how C++ adopted 2's complement (even though C followed that decision later).

JS: Aren't there `printf` macros too?

GB: I think so; I'll double-check whether those are included automatically.

NR: I hear (absent objection) that we don't have major concerns here, and that WG14 can pick this up later.

### P2142 Allow '.' operator to work on pointers

(JB presents P2142R1.)

JB: My paper based on C++17.

JB: Beginning programmers at my most recent company still had trouble recognizing the need for `->`.

VV: We can't make this change for smart pointers.

JB: It's not an error to use `.` with them.

VV: But it's not the same as `->` there, and we don't want to mix their meanings.  Who would actually be helped when avoiding raw pointers?  The improvement is too late.

JM: It's a fundamental difference (Java notwithstanding) and a non-starter.  Maybe WG14 wants the idea, but why discuss this in SG22?

PM: The Linux kernel developers actively don't want this; `->` heralds a potential cache miss and allowing `.` hides errors.  The requirements for C are not the same as high(er)-level language. 
We'd have to wait years to use it anyway.  The beginning-programmer mindset described is incompatible with producing quality kernel code.

JB: I had an algorithm in C and could change it into Javascript just by replacing `->` with `.` and `int` with `var`.  It would be nice to go backwards.

PM: The forward direction is a trivial change.

JB: Yes, a pointer can have an additional expense.

JB: I'll drop the paper; WG14 was interested if WG21 was.

NR: We have people from WG14...

JG: We would never add something without existing compiler support, and their customers haven't demanded this.  The beginner problem is not the syntax, but the abstract notion of a pointer.

NR: This probably can't proceed in WG21, but are there more comments from WG14?

PP: `->` is used in C++ for many things beyond pointer indirection.

JS: If we could have `operator.`, this might make sense.

VV: It's attractive, but we'd need a time machine (or a third syntax that wouldn't match Java/Javscript).  We also can break programs by making existing syntax no longer ill-formed.

AB: I agree with Ville, but to extend what Paul McKenney said: we could downgrade the error to a warning, but users appreciate the feedback.

NR: We don't approve papers, but EWG (which does) is unlikely to approve this.

JB: In C, a generic operator allows more generic usage.

AB: WG14 tends to be very conservative with field experience (as Jens Gustedt said).  I don't know what the Clang community with an RFC on this subject, but there would probably be pushback even just for C (partly because of things like Objective C).

VV: Most users wouldn't dare to request language extensions, and compiler authors aren't keen on extensions in fundamental areas, so it would be hard to get implementation experience here.  There's a chicken-and-egg problem between the committees and the compiler implementers.  We don't have good information about what users want (but perhaps it's a good thing that compilers don't implement just any idea).

JB: Open Watcom supports DOS with weird pointer sizes.  The patch would be minor.

NR: We're running out of time.  Jim, do you have any questions?

JB: No; thanks for the conversation.

JS: Is SG22 meeting in Hagenberg?

NR: We don't meet in person because we wouldn't have WG14.

NR: I'll schedule another teleconference once we have papers identified.

# January 7th, 2025
## Agenda
- [P3477R0 There are exactly 8 bits in a byte (JF Bastien)](https://github.com/cplusplus/papers/issues/2131)
- [P3475R0 Defang and deprecate memory_order::consume  (Hans Boehm)](https://github.com/cplusplus/papers/issues/2129)
- [P3384R0 COUNTER (Jeremy Rifkin)](https://github.com/cplusplus/papers/issues/2041)

## Attendees
- Nina Dinka Ranns - Chair
- Joshua Cranmer 
- Jens Gustedt - Scribe
- Rajan Bhakta (IBM)
- Jeremy Rifkin
- Hans Boehm
- Paul E. McKenney
- Ville Voutilainen 
- Jens Maurer
- Robert Seacord

## Meeting Summary

P3475R0 Defang and deprecate memory_order::consume 

Hans Boehm presents.
--------------------

defang ~ make it less dangerous
consume was introduced C++11/C11 but was never really implemented
The reason was to make it easier to write lock-free code, e.g RCU idiom. But technically the consume model was never necessary because architectures do the update of dependent data.
In the field the model was never completely implemented.
It was already proposed to be deprecated in C++17, but then the attempt failed. But since not much has happened on the implementation side, Hans reproposes again.
On the other hand the memory model needs reform and consume complicates the arguments.
Even on ARM processors the difference is not relevant any more.
The paper simplifies the C++ text quite noticeably.
Existing code should be preserved.

Rajan: I talked to our teams and IBM is good with it.

Jens G.: all for it for the C memory model

Paul: linux kernel has something similar to kill_dependency but do not use the C feature

Proposal to push it also to WG14

Consensus to proceed.

P3477R0 There are exactly 8 bits in a byte
--------------------
Robert Seacord presents.

No one has answered this in interview questions correctly.
There is some hardware that has more than 8 bits in a byte.
There is a clear argument to restrict this value for C++, but for C the argument is a less weaker because there are more compilers around

Ville: there are DSP by TI with 24 bit processors, but there is no plan to do more than C++03 on that platform. He has no idea if their C compiler is modernized to be relevant.

Jens M.: possible avenue would be that C++ goes ahead

Joshua: some people come from time to time to propose more than 8 bits in clang

Jeremy: would it still be possible to have C++ compilers with more bits? 

Ville: probably … you would have to emulate that

Jens G.: recently we had problems in C for the bit-op functions, so doing something similar would really help

Jens M.: gcc still has the flag, so you could implement it relatively easily, but that is really unlikely that someone would really do that for C++, in the past 10 year nobody cared

Ville: DSP do parallel processing and you wouldn't do text processing, it is really special hardware

Jens G.: in C, resticting to 8 bit for hosted environments would probably the most convenient to do, freestanding could have a bit more possibilities

Consensus to proceed

p3384 __COUNTER__
--------------------
Jeremy Rifkin presents:


It is used quite a lot of places, mostly for unique identifiers.
There are alternatives in C++ with templates, but not in C.
Not propagated across module boundaries.
Question is about how often this would evaluate? In C++ all compilers agree, in C there is some deviation.
Counter range? The type would jump at boundaries of the signed types.

Jens G: - decimal literals should be defined different - use perhaps INT_MAX as a minimal guarantee

Jens M.: when it overflows the maximal value, the program is illformed, so compilation is usually aborted

Robert: has questions about using unsigned

Ville: there will be antibodies activated in the C++ community, so maybe it is better if this goes into C first

Jens G.: would they prefer to have in C first, so they don't have to worry about it?

Jens M.: It is already there in the field for C++. But we would need to have the specification to match reality.

Ville: Suggests to primarily go through WG14.

Consensus to proceed.

# August 28th, 2024  
- Topic: P3309 and P3140
- Start: 03:02 UTC
- End: 03:43 UTC

## Agenda
- [P3309 R1 constexpr atomic and atomic_ref](https://github.com/cplusplus/papers/issues/1960)
- [P3140 std::int_least128_t](https://github.com/cplusplus/papers/issues/1793)

## Attendees
- Nina Dinka Ranns - Chair
- Davis Herring
- Corentin Jabot 
- Joshua Cranmer
- Jens Gustedt 
- Vlad Serebrennikov
- Davis Herring
- Jan Schultke
- Hana Dusíková
- JeanHeyd Meneide - Scribe
- Jens Maurer
- Davis Herring
- Walter E Brown

## Meeting Summary

P3309r1: constexpr atomic<T> atomic_ref<T>
Hana Dusíkova
------------

Hana: (* starts off by explaining the paper and its purpose and its implementation *)

Nina: Jens?

JensG: Yeah this does not collide with anything in C because we don't even have constexpr for functions in C. Just one semantic question: we have atomic_wait and we are marking this constexpr, do we know why we need to mark this constexpr specifically?

Hana: It just doesn't do anything, its treated as a wait in a single-threaded program (* Hana browses to the literal patch in llvm-project/libcxx to show it)

JensG: Ah so just an atomic wait in a single-threaded program just... does nothing?

Hana: (* finds the implementation of `wait` in `atomic<T>` in her branch *) yes, so, we just do a load check, and if it doesn't give us the right value, we do a `__builtin_trap()` which, in this case, just stops compilation with an error.

JensG: Okay, okay, yeah that's fine.

Nina: Any other comments? Any other questions? Any concerns about the compatibility ?

(* room goes silent, someone chimes in with "No" *)

Nina: Okay, perfect.



P3140r0: std::int_least_128t
Jan Schultke
--------------------

Jan: (* presenting *) yeah the reason for this paper is just to add 128 bit integers to C++. We can see around 145K usages of some form fo int128/int_128 as a type, which is the same order of magnitude of long double. EWG and specifically Bjarne said they need 128 bit integers. The way we were going about this is just doing a hack it into the library through <cstdint>. C23 made some changes which eliminated the intmax_t problems. My only concern is how this will end up looking for C: is there any compatibility concerns if we add std::int_least128_t but no int_least_128_t.

Nina: JeanHeyd?

JeanHeyd: Yeah Jens Gustedt already fixed up the ABI problem as you mentioned. We have support for "%w128d" printf modifier already in C, so that solves that problem.

Nina: Okay. Jens?

Jens: So there's one thing we need to worry about and its really alignment between the two languages (* SCRIBE'S NOTE: literally like `alignof(std::int_least128_t)` *). This also might pose a problem in freestanding for both C and C++, as the hardware support just might not be there for this.

Jan: Yeah, I received a lot of feedback about this and so ultimately we took it from being required everywhere to only being required for hosted implementations.

Vlad: What does this mean for the .h headers? I think we own the <cwhatever> headers and can make changes to them, what about the <stdwhatever.h> headers?

JensM: So this is actually correct except for the portion that the ".h" headers are ALSO C++ headers. The implementation details and similar were sorted out a while ago. (* SCRIBE'S NOTE: this is a reference to a meeting around LEWG about updating C++ to handle C changes in the library, and where headers are sourced from in C++ implementation and what it meant. *) Modifying those headers (the ".h" headers) is fine.

Jan: Okay, good, because that was my understanding.

Vlad: You should also update section 4.1.3 because it's not fully in sync?

Jan: This is moreso a suggestion about C, not what the changes are to be made by the C++ version of the proposal.

Jens: If you want to keep this advice up to date, there's other places you need to suggest to make changes such as <stdckdint.h>. We should also see a proposal of this at some point in WG14, but there is no blockers for C++ to move forward on this.

Jan: Yeah, we also need to do <stdbit.h>

Nina: Corentin?

Corentin: A clarifying question, especially for C. Are you saying we want this to be added in a different way to handle this in ADDITION to having _BitInt(...), for C?

JensG: Yes, it is okay to have this support.

JeanHeyd: (* ridiculously long explanation of implementations which support _BitInt at the lowest allowed value (BITINTMAX == 64) but still also have extended integer types like int128, since some implementations have expressed annoyance at implementing algorithms to handle not just the powers of 2, but EVERY bit size between 1 and BITINTMAX *)

Nina: Okay... any other comments? Any concerns over compatibility ?

(* long, slow silence *)

Nina: Alright, then I think that means we're done!


# July 26th, 2024

- Topic: P2865 and P2866
- Start: 17:05 UTC
- End: 18:11 UTC

## Agenda
- [P2865 Remove Deprecated Array Comparisons from C++26 ](https://github.com/cplusplus/papers/issues/1555)
- [P2866 Remove Deprecated Volatile Features From C++26](https://github.com/cplusplus/papers/issues/1556)

## Attendees
- Nina Dinka Ranns (Chair)
- Corentin Jabot (Scribe)
- Vlad Serebrennikov
- Aaron Ballman 
- Joshua Cranmer 
- Ville Voutilainen 
- Michael Wong 
- Hubert Tong 
- Alisdair Meredith 

## Meeting summary
P2865 - making array comparison array ill-formed

Aaron: Not deprecated in C, don't know if C would want to do this. C usually doesn't like special cases. No compatibility concern but implementation will have to support that anyway

Ville: There are work around possibles - so a subset of compatible code remains. Will lead to clearer code in C++

Aaron: Agree with ville. because it appears in expressions, it appear less in headers

Ville: C++ will be stricter, it's not a new problem. The sky has never fallen

Nina: Does anyone want to bring that to C? Would anyone in WG14 object

Aaron: I am not aware of anyone objecting - not time to write a paper but happy to present one

Ville: the paper has no deployment experience.WG14 would probably appreciate having that experience and data on code in the wild.

Alisdair: I am not qualified to bring it to WG14

Nina: We will put that on the list of things WG14 might want to see, with an encouragement to provide implementation experience

[The room silently agrees that they do not have compatibility concerns with P2865]


—

P2866

[Alisdair presenting]

Hubert: You said this is deprecated in C but i could not find wording for that

Alisdair: I might have been misled

Aaron: WG14 considered N3743 - the goal was to align with C++ - and we rejected it. No C compiler diagnoses these, which WG14 took as a signal that this was not an issue. As an implementer i don't see a motivation for removal as we will have to support it forever. 
WG14 thinks the volatile semantics is fine here
But I don't have compatibility concerns.

Ville: same comment as for P2865 - not real compatibility concerns, there are work around.

Aaron: Nobody's C front end diagnose misuse

Ville: Well, it's not really possible to diagnose misuses, deprecation warnings don't have that problem. The lack of warning therefore is not really an indication of appetite or lack thereof.


[Moving on to volatile parameters]

Hubert:This paper claim volatile on parameters is meaningless because the compiler can see the whole lifetime, but there are valid use cases (signal handling, longjmp)

A claim was made that volatile on parameters leaks implementation details, but signature don't have to match (even if the microsoft abi does not respect that).
I have use cases that cannot be worked around.

Ville: correct, some functionality cannot be expressed differently.
Generally, WG21 is trying to move away from volatile types. We just want volatile accesses and we want to do that.
This is why we probably would not want to undeprecate volatile parameters.

Hubert: The 2 prior uses cases for volatile parameter cases
setjmp/longjmp - if you don't use volatile, jumping back in a function, would not reliable observe the value
to reliably observe the change of a value in a signal handler

Aaron: another use case is volatile sigatomic_t


Nina
Will go back to EWG
If we remove volatile parameter, or undeprecate them, does it affect how we feel about compatibility

Ville: Deprecating would increase compatibility - but C++ compilers can decide volatile parameters don't do anything because people rely on a behavior that is unspecified. This is implementation ascribing their own behavior. No appetite to keep supporting these use cases at the cost of keep being on the path of getting rid of volatile qualified types

Hubert: But it is in the C standard, so this is why compilers provide this behavior. This change might break C headers as implementations might volatile qualify sigatomic_t.

Ville: The compatibility problem always existed, specification-wise. 
I have always found it unwise to rely on that unspecified behavior. These use cases were never the original intent of volatile.


Nina: do we need to bring any compatibility concerns to EWG

Ville:  Yes because of what hubert mentioned - for both parameters and return types

Hubert: Agree

Alisdair: If EWG rejects Hubert, and keeps with removal, are we expressing objection?

 Ville: If we don't do that removal, it doesn't hurt anyone and we could consider doing it later. Removing this clause C.7.6 part from this paper and keeping it deprecated doesn't hurt

Nina: No objection to striking that clause

[Room nodes]

[Alisdair requests help to explain the issue]

[No taker]

Nina:
It would be better to bring a more complete analysis of this issue.


## Polls

- Sg22 recommend undoing removal of volatile qualified parameters and return types

SF: 4 | F: 2 N 2 | A: 0 | SA: 0



# February 1st, 2024

- Topic: Provenance Memory Model Discussion between C and C++
- Start: 17:05 UTC
- End: 18:11 UTC

## Agenda
[P2318: A Provenance-aware Memory Object Model for C](https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2021/p2318r1.pdf)
[P2434: Nondeterministic pointer provenance](https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2022/p2434r0.html)

## Attendees
- Nina Dinka Ranns (Chair)
- Freek Wiedijk
- Gabriel Dos Reis
- Davis Herring (Author, Presenter)
- Giuseppe D'Angelo
- Jens Gustedt (Author)
- Joshua Cranmer
- Kayvan Memarian (Author)
- Martin Uecker	(Author)
- Nathan Owen
- Michael Wong
- Peter Sewell (Author)
- Inbal Levi
- JeanHeyd Meneide (Chair, Scribe)


## Meeting summary
- Davis Herring: We can discuss one paper or another if people have familiarity, but we can start by discussing both papers and then dovetail into P2434R0 (Scribe Note: P2318 is an)
- Jens: I can give an overview of P2318 and its current status
	- Came out of long process for C and its memory model study group, met with C++ in Köln (Scribe Note: English spelling is Cologne, in Germany) in some ways to discuss this
	- WG14 chose a model that they would like to apply to their standard (model name: PNVI-ae-udi)
	- Difficulty with ISO accepting the TS that sourced P2318, and so that results in the current status where it is not fully published as its own TS
	- We will publish a new TS that textually describes what is in front of us with P2318r1 and its diff.
- Nina: And so this would just be a TS?
- Jens: No, not in the standard or C23, just in a TS. We took a vote and it should get into the standard in C2Y, but it depends on the feedback of the TS (Scribe Note: not guaranteed to go into C2Y).
- Nina: Is there implementation experience of this?
- Jens: Not really necessary for implementation experience, this is supposed to be more or less be a solidification of existing practice modulo divergences and bugs for C compilers and their memory (and "object") models with how Effective Types are used.
- Peter: To add on, we would like to ensure that we do not break any existing implementations and their code. Nonetheless, some of the compiler developers have already pointed out things that may be bugs in their implementations and they want a more rigorous model to fully test against code.
- Joshua: As an implementer (Scribe Note: Intel, US), a lot of what we proscribe likely matches but we want to get some time to really check our implementations. For LLVM, there are a few places where we e.g. do pointer-to-integer and integer-to-pointer that do not seem to follow this specification. So we need to check which is why we wanted a TS and not straight into the standard.
- Nina: So... does that mean the LLVM code is buggy against this spec?
- Martin: Not necessarily, it's a bit more nuanced. The optimizers are not consistent with themselves, so we agree generally there are bugs. But we do not know exactly how they need to resolve such bugs or issues, which brings us to the TS trying to more rigorously specify that so we can all agree on the answers.
- Nina: OK. So can anyone can explain the difference between the C TS versus the P2434r0 (Nondeterministic pointer provenance).
- Davis: Okay, so I can do that. For starters, I just want to clarify that I am not trying to compete or eliminate the work done by C. This is not meant to be divergent or split from how C does this work, it just wants to answer a few of the questions in the way that makes sense, especially for C++. In particular, I am saying that the work is significant, the specification done in the C TS is significant, and that there's a small bit of work that can be done to get it closely in line. Particularly, I think the "udi" part of "PNV-ae-udi" is the bit that is not possible fully for C++. Can... I present?
- Nina: Ah, can I pass you the presenter?
- Davis: (Scribe Note: Davis cannot present from his current location and setup, Nina agrees to display the paper P2434r0 on the screen.)
- Davis: (Scribe Note: explanation of the paper which is effectively reading from it and narrating the logic shown in the examples and written down in the paper.)
	- … It is nondeterministic to observe the pointer there, and what we want to do is get rid of that part of the specification and simply leave it as undefined behavior or as close to that as possible without a rigorous specification of exactly how we arrive at that conclusion (so-called "angelic nondeterminism")—
- Peter: (Interjecting) What you're describing is exactly what PNV-ae-udi, so I am confused as to why we want to get rid of that specification here especially if we're arriving at the same answer...?
- Davis: I am not suggesting we should, that's good! We're just saying we can get to the same point with less provenance and less modeling here.
- Peter: Well... okay, just continue.
- Davis: Observe this XOR swap of the integer value of these two pointers (using uintptr_t). The problem with this is that, eventually, it says that if you "guess" the right value of a pointer as an integer, this leads to technically no longer being UB but being Defined Behavior (in the udi model). This can present some problems with the optimizers and it means that the compiler gets stuck because someone could do all sorts of things with this behavior, including write the pointer value and read it back from a file or over the network and as long as they read back the right value they are supposed to be able to treat this integer-turned-pointer as having been correct the whole time without knowing it could be correct.
- Jens: Our intent really was the opposite here. We wanted to say that such behaviors were illegal in the goal that optimizers would be able to optimize around it with a set of rigorous rules.
- Davis: My goal is to really just change the "ae" and make it so we do not need to specify it directly and leave it nondeterministic from the surrounding wording. This is important because the reasoning of how we get here could impact the way optimizers work and thats why we want to have nonangelic determinism here rather than rigorously specify ae-udi (of PNV-ae-udi).
- Martin: We want to have semantics that **allow** someone to extend the semantics of the machine to hold on to behaviors that users do. And so the goal is to explicitly define the "ae" (specifically exposure mechanisms) so that implementers and users can agree on specific explicit exposure mechanisms so they can get more well-defined behavior. We don't want to just leave this entire space UB because even if we gain optimizations for a compiler without needing tracking we can lose a lot of folks that need the well-defined behavior (through the exposure mechanism).
- Peter: I just want to say we have not fully rejected non-determinism. In many ways the current design of PNVI-ae-udi is to allow this if implementations want to this.
- Davis: Certainly, we want to bless specific pointers for interesting, non-Standard use cases (Scribe's Note: typical hardware pointers, magic register pointers, magic file/OS pointers, clocks, timers, etc.). Implementations are always in the business of specifying certain undefined behaviors for practical purposes. E.g., Address Sanitizer will trap on a bad address access, and that's because they clamped down on UB. This also happened with the initialization of all automatic storage variables to be 0-init, where losing the UB means we are taking away the checking of the variable.
- Peter: I think I want to really point out that the provenance model is to allow the abstract machine to identify that UB to make their behavior as they desire.
- Davis: Yes, I was responding to what Martin was saying; we want to just use UB, we do not need to **specifically** call out the exact tracking mechanism for such UB. We just want to call it all UB. This will leave compilers with all of their room to manuever
- Martin: So I agree on a high-level of this, where we want UB to be there. But we need to provide a more targeted mechanism to allow for that UB to identified, AND without an exposure mechanism (Scribe note: the "ae" of PNVI-ae-udi) then it is not clear how to either clamp down on the UB or otherwise enumerate useful possibilities because it will be too wide. Having the analysis and exposure mechanisms specifically called out helps give C programmers the exact tools in conjunction with their implementations to get this correct.
- Jens: If you take a pointer value and cast it to uintptr_t, it is not possible to do proper aliasing analysis. We just want to make sure that part is in there.
- Davis: The problem here with this model is that if there's a cast from a pointer to a uintptr_t means that there might be some notional idea of state in the virtual abstract machines. I want to eliminate that notional idea of state and reach the same answer as PNVI-ae-udi without being that specific or require that notional idea of the state that might need to be tracked or carried through.
- Peter: So I think the only issues with the angelic nondeterminism is that it becomes very, very hard to compute -- sort of mathemtically -- the kinds of programs we can have predictable programs that users can rely on, epecially without some kind of exposure mechanic or similar.

(Scribe note: we begin talking about the superposition of interpretations of pointers here and this is where the Scribe starts getting very lost.)

- Davis: So this is problematic because specifying how the set of values that computes the superposition of pointer values, and then casting it from an integer back to a pointer we collapse that down into a single pointer and you have to pick an interpretation from all of those potential (valid, invalid, etc.) superpositions.
- Peter: So I think the difference between the reasonings between this paper and the C TS is that one is the superposition of all pointer values	and provenances that eventually gets collapsed into one (P2434, angelic nondeterminism), versus the interpretation that there a superposition of all interpretations of provenances that get projected forward to figure out the right one (e.g., the user compared the integer values from the pointers and found they were correct, P2318, effective types).

(Scribe Note: Davis and Peter go back and forth and at some point this gets into concurrency with provenance models and such, and at this point the scribe is now lost. Apologies.)

- Peter: I am not sure the implicit object creation (with concurrency) is a rigorous enough model to write specification against, even if in text it is possible.
- Davis: It is something I am still studying and researching with respect to concurrency and UB, and we might need to be looking more into trying to define UB here for what triggers it exactly.

(More discussion on the inconsistencies in various compilers with regards to this.)

- Peter: If there's to be any hope to find out how we can deal with UB in these circumstances, starting with divergent specifications (Scribe's note: specifically between C and C++) would be a bit bad.
- Nina: It's a bit hard to do that, but it's okay if an incompatibility emerges that we document it so its known and we both know we made the decision fully informed.
