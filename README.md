
# SG22 Compatibility

Welcome to the SG22 C & C++ Compatibility Repository. Here you will find meeting minutes, presentations, notes, documentation, and tracking for various compatibility issues between C and C++.

Go through the [issues list here](https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues) if you want to see if there is a compatibility issue that is open for something you care about. Look at the [closed issues list](https://github.com/sg22-c-cpp-standard-compatibility/sg-compatibility/issues?q=is%3Aissue+is%3Aclosed) to see if this is something that has already been addressed.

# Chairs

- Nina Dinka Ranns (primarily Working Group 21 - C++)
- [JeanHeyd Meneide (primarily Working Group 14 - C)](mailto:wg14@soasis.org)

Feel free to contact us when necessary.


# Useful Reading

- For a good, high-level overview of C and C++ compatibility issues and (intentional) divergence, see Aaron Ballman's excellent [P2735 - C XOR C++](https://wg21.link/p2735r0).


# SG22 2024 Meeting Summaries

This document contains summaries of SG22 meetings held during 2024.

- [February 1st, 2024](#February-1st-2024) - Provenance and Memory Model Discussion
- [July 26th, 2024](#July-26th-2024) - P2865 and P2866

# July 26th, 2024

- Topic: P2865 and P2866
- Start: 17:05 UTC
- End: 18:11 UTC

## Agenda
- [P2865 Remove Deprecated Array Comparisons from C++26 ](https://github.com/cplusplus/papers/issues/1555)
- [P2866 Remove Deprecated Volatile Features From C++26](https://github.com/cplusplus/papers/issues/1556)

## Attendees
Nina Dinka Ranns (Chair)
Corentin Jabot (Scribe)
Vlad Serebrennikov
Aaron Ballman 
Joshua Cranmer 
Ville Voutilainen 
Michael Wong 
Hubert Tong 
Alisdair Meredith 

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

Nina:

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
