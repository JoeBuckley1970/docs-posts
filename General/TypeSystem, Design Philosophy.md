# SHORT VERSION:

![LinkedIn](https://img.shields.io/badge/LinkedIn-Post-blue?logo=linkedin)

**Modeling big systems can be tough. Even though the root question is simple…**

**What is a thing?**

Philosophers have disagreed for centuries:

* It’s a substance that *has* properties. (Aristotle)
* It’s just a bundle of attributes. (Hume)
* Or it’s something our mind synthesizes from attributes into an identity. (Kant)

When we design software, we implicitly pick one.

Object-oriented systems assume the “thing” comes first, and properties live inside it.

A pure Bundle Theory approach is difficult to realize. Attributes need something to be about — without a bearer, they lack stability.

Most modern languages allow bundles (interfaces), but here’s the tension: 
If two interfaces define a property called `Cost`, and an object references both, is it one `Cost` or two?
In most systems, it’s resolved by convention.

Lately, I’ve been exploring a different inversion.

Instead of starting with **Object -> Property**
what if we start with **Attribute -> Entity**?

I call this **Attributes-Orientation**.

* **First-Class Attributes:** An attribute like `Cost` exists independently, with its own identity and meaning.
* **Entities as Bearers:** An entity simply holds attribute–value pairs.
* **Types as Bundles:** A type is just a named bundle of shared attributes.

In that model, `Cost` has one identity. Types merely reference it.

I’m still refining this idea. But the more I work in knowledge modeling, the more I suspect identity is not where we think it is.

#KnowledgeManagement #SoftwareArchitecture #TypeSystems #SystemsThinking


---
# LONG VERSION:

# TypeSystem, Design

## The Philosophical Perspective

### What Is a Thing?

- **Aristotle's Substance Theory:** A thing is a **substance** — a unified entity that serves as the underlying subject for its properties. It exists independently. Some properties are **essential** (defining what it is), while others are **accidental** and can change without affecting its core identity. **E.g.,** When a car changes from red to blue, it remains the same car because the substance (its "car-ness") persists.

- **Hume's Bundle Theory:** A "thing" is nothing more than a **bundle of perceptions/attributes**. There is no underlying "bearer" to hold them together. The entity is logically constructed from its sensible qualities. **E.g.,** When the car's color changes from red to blue, one bundle of perceptions has ended and a new, different bundle has begun — so, in a strict metaphysical sense, it is a different "car."

- **Kant's Transcendental Idealism:** We can never know things as they are in themselves (noumena). We only experience them as **phenomena**, which are appearances synthesized by our mind's innate structures (space, time, causality). The mind actively combines sensory attributes into a coherent object of experience. The question of the object's identity is not found in the world but is a **judgment** we make. **E.g.,** When the car changes from red to blue, we don't perceive "sameness" directly; instead, our mind allows us to **judge** that it is the same car, even though the raw sensory data is different.

### So What?

This philosophical debate isn't just academic — it's a mirror of the choices we make when designing type systems.

1.  **The Aristotelian Legacy:** Most object-oriented languages are built on an Aristotelian foundation. We start with the **thing** (the object or class), and its properties are secondary, defined as an afterthought within that fixed container.

2.  **The Humean Impasse:** A pure Bundle Theory approach is difficult to realize. Attributes need something to be about — a subject, a context, an identity. Without a bearer, they lack a stable reference point. We can’t build systems on pure flux.

3.  **The Kantian Compromise (and Its Limits):** Modern systems have intuitively arrived at a Kantian compromise. We acknowledge that the "thing" is a judgment call. We use **interfaces** to bundle related attributes and then mix and match these bundles to define a **type**.

    - We can define `IAsset(Value, Depreciation)`, `ITransport(Speed, Convenience)`, `ICar(Make, Year)` and then define `Sedan : IAsset, ITransport, ICar`.
    - This is powerful — it lets us construct our perception of an object from meaningful attribute bundles.

    But this compromise has a critical flaw: **Attributes are still second-class citizens.** They are trapped inside the interfaces that define them.

    Consider the attribute `Cost`. If you have an `ITransport(Cost)` and an `ICar(Cost)`, is that the same attribute or two different ones? In most languages, this is resolved by convention (and namespacing) at best and silent conflict at worst. The attribute's identity is lost, defined separately within the silo of each type that uses it.

### A New Path: Attributes-Orientation

We need a model that is stronger than convention. I propose a system that inverts the traditional hierarchy, taking the Kantian insight to its logical conclusion: **if our perception of an entity is a synthesis of attributes, then attributes should be the foundation.**

I call this an **Attributes-Orientation** (to contrast with Object-Orientation).

- **First-Class Attributes:** An attribute definition — like `Cost`, `Color`, or `Speed` — is a first-class citizen. It exists independently, with its own identity and meaning, outside of any type or entity.

- **Entities as Bearers:** An entity (the "bearer" of attributes) can then have a value for an attribute without needing to belong to a predefined type. An entity is, in a sense, a unique bundle of attribute-value pairs.

- **Types as Bundles:** A type is simply a named bundle of these first-class attribute definitions. `ITransport` is a bundle containing the `Speed` and `Cost` attributes. `ICar` is a bundle containing the `Make`, `Year`, and `Cost` attributes.

This simple inversion solves the core problem: **Attribute identity is preserved.**

Because `Cost` is a single, globally identifiable attribute, an entity that is typed as both `ITransport` and `ICar` does not end up with two different `Cost` values. It simply has one `Cost` attribute, which satisfies the requirement of both bundles that reference it.

> A side note on terminology: Since object-orientation uses the terms `Object` and `Property` by convention, I propose we use the terms `Entity` and `Attribute` when developing attribute-oriented systems.

In an attempt at brevity, I have not talked about actions. But suffice to say that actions are also first-class citizens in the system and can be used to define behavior on an entity. But that's for some other time.

This is not an entirely novel idea — systems like ThingML and OpenMDAO, Topic Maps, Entity-Component-Systems, and many others have elements of this. 

I’m still refining this idea. But the more I work in knowledge modeling, the more I suspect that identity is not where we think it is.

#KnowledgeManagement #SoftwareArchitecture #TypeSystems #SystemsThinking
