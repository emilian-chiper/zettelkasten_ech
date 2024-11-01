### Meta
2024-10-24 13:16
**Tags:** [[c]] [[c_getting_started]]
**Status:** #completed 

### Portability
Programs written for C can be considered *strictly conforming* if they use only those features of the language and library specified in the standard. These programs are intended to be maximally portable. No real-world C program is strictly conforming. Instead, the C Standard allows you to write *conforming* programs that may depend on nonportable language and library features.

Five kinds of portability issues are enumerated in Annex J  of the C Standard documents:
- Implementation-defined behavior
- Unspecified behavior
- Locale-specific behavior
- Locale-specific behavior
- Common extensions

#### Implementation-Defined Behavior
*Implementation-defined behavior* is a program behavior that’s not specified by the C Standard an that may offer different results among implementations, but has consistent, documented behavior within an implementation. An example of implementation-defined behavior is the number of bits in a byte.

Implementation-defined behaviors are mostly harmless but can cause defects when porting to different implementation. Whenever possible, avoid writing code that depends on implementation-defined behaviors. Check Annex J.3 of the C Standard for more details.

You can document your dependencies on these implementation-defined behaviors using a `stattic_asser` declaration.

#### Undefined Behavior
*Undefined behavior* is behavior that’s not defined by the C Standard, or “behavior, upon use of a nonportable or erroneous program construct or of erroneous data, for which the standard imposes no requirements.”

Examples of undefined behavior include signed integer overflow and dereferencing an invalid pointer value. Code that has undefined behavior is often erroneous, but with some nuance.

Undefined behaviors are identified in the standard as follows:
- When a “shall” or “shall not” requirement is violated, and that requirement appears outside a constraint, the behavior is undefined.
- When behavior is explicitly specified by the words “undefined behavior”.
- By the omission of any explicit definition of behavior.

The first two kinds are frequently called *explicit undefined behaviors*, while the third is called *implicit undefined behavior*. There is no difference in emphasis among these three. See C Standard Annex J.2, “Undefined behavior” for more details.

Developers often misunderstand undefined behaviors as errors or omissions in the C Standard, but the decision to classify a behavior as undefined is *intentional* and *considered*.

Behaviors are classified as undefined by the C Standard committee to do the following:
- Give the implementer license not to catch program errors that are difficult to diagnose.
- Avoid defining obscure corner cases that would favor one implementation strategy over another.
- Identify areas of possible conforming language extension in which the implementer may augment the language by providing a definition of officially undefined behavior.

These are considered portability issues.

Compilers have the latitude to do the following:
- Ignore undefined behavior completely, giving unpredictable results.
- Behave in a documented manner characteristic of the environment (with or without issuing a diagnostic).
- Terminate a translation or execution (with issuing a diagnostic).

It’s best to avoid undefined behaviors except when the implementation specifies these behaviors are defined to allow you to invoke a language augmentation.

#### Locale-Specific Behavior and Common Extensions
*Locale-specific behavior* depends on local conventions of nationality, culture, and language that each implementation documents. Common extensions are widely used in many systems but are not portable to all implementations.