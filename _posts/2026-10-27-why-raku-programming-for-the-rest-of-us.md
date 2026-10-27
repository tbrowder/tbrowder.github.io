---
layout: post
title: "Why Raku? Programming for the Rest of Us"
date: 2026-10-27
categories: [raku, programming]
published: false
---

*Part 1 of 2: An invitation to program, whether or not you want a programming career.*

Programming should not belong only to professional programmers. A student in mathematics, a retired engineer, a scientist examining measurements, or a curious hobbyist can benefit from writing small programs. Sometimes all we want is a computer that will ask for a few numbers and give us a useful answer.

I think [Raku](https://raku.org/) deserves consideration for exactly that kind of work. Python is deservedly popular, with a remarkable range of scientific libraries. But I find Raku unusually comfortable for *writing my own* little tools. Here are a few reasons.

## A confession from a hunt-and-peck typist

I've used computers for years, but I'm still a hunt-and-peck typist. Keyboard convenience matters to me. Python commonly writes a descriptive name as `total_cost`; in Raku I can write `$total-cost`. I can press the hyphen key without Shift. Raku's `$` sigil and statement-ending semicolon mean it doesn't always use fewer keystrokes, but I like the immediate visual clues, and I like having a choice.

I also like the freedom to lay out my code. Python uses indentation to delimit blocks; Raku generally uses braces. I still indent carefully because readable code matters, but I don't want indentation to determine the program's structure. Raku's whitespace is not *always* insignificant; some syntactic distinctions do depend on spacing.

## Start with a useful calculation

Suppose we want the area of a circle, $A = \pi r^2$. Save this as `circle.raku`:

```raku
#!/usr/bin/env raku

my $radius = prompt("Enter the radius: ").Num;
my $area = pi * $radius ** 2;
say "The area is $area";
```

Run it with `raku circle.raku`. There is no project template, class hierarchy, or framework to build first. `prompt` asks a question, `.Num` converts the answer, `pi` supplies the familiar constant, and `say` prints the result. This deliberately simple example assumes valid input; later we can check for invalid numbers and negative radii.

The Python equivalent is also straightforward:

```python
import math

radius = float(input("Enter the radius: "))
area = math.pi * radius ** 2
print(f"The area is {area}")
```

Both languages can do the job. Raku's prompt, interpolation, and numerical vocabulary feel especially natural to me.

## Arithmetic for the curious

Consider a couple of one-line experiments:

```raku
say (1..100).sum;               # 5050
say [+] (1..10).map({ $_ ** 2 }); # 385
```

The range `1..100` means exactly what it looks like. The second expression squares numbers from 1 to 10 and adds them. Raku has plenty more to explore: sets, bags (multisets), sequences, and operators that work across collections.

Ordinary decimal arithmetic can also be pleasant:

```raku
say 0.1 + 0.2 == 0.3;  # True
```

Raku ordinarily uses a rational representation for decimal literals, avoiding many familiar binary floating-point surprises. That does **not** mean all Raku arithmetic is unlimited-precision or that numerical error disappears: `Rat` has limits, and numerical work still requires choosing the right types and methods. Python offers precise arithmetic too, through `decimal` and `fractions`.

For students, these distinctions can be a fine reason to experiment: *how does a computer represent a number?*

## Text processing without a forest of punctuation

Mathematics and science involve more than arithmetic. Data arrives in text files, instrument logs, lab notes, and tables. Raku has powerful regular expressions and grammars built into the language.

```raku
my $line = "Sample number 42";

if $line ~~ / <digit>+ / {
    say "Found: $/";
}
```

That pattern finds one or more digits. Larger Raku patterns can be organized into named rules, making it possible to describe structured data or even a little language for mathematical formulas. Python's `re` library is capable too; Raku's pattern language is one of its distinctive pleasures.

## Unicode belongs here

Mathematical writing is full of symbols, and Raku treats Unicode as an integral part of its world. You can use Greek letters in identifiers:

```raku
my $α = 3;
my $β = 4;
say $α + $β;
```

You needn't type Greek to use Raku. I ordinarily prefer plain ASCII myself. Still, it is good to have Unicode available, including support for grapheme clusters—the characters people see on the page, which don't always correspond one-to-one with Unicode code points.

## More than one way to do it

Perl gave Raku a useful philosophy: *There's more than one way to do it.* These three loops print the same numbers:

```raku
for 1..5 -> $number {
    say $number;
}

for 1..5 {
    say $_;
}

.say for 1..5;
```

A beginner can favor the first, explicit version. A programmer comfortable with Raku may choose another. I appreciate that the language accommodates both. The tradeoff is that someone reading unfamiliar Raku code may encounter more stylistic variety.

## Classes when you need them

You may eventually want to keep measurements together with the operations that use them. Raku's classes are compact:

```raku
class Measurement {
    has Str $.name;
    has Numeric $.value;

    method report() {
        say "$!name = $!value";
    }
}

my $sample = Measurement.new(
    name  => "Temperature",
    value => 98.6
);

$sample.report;
```

There is no need to begin with classes. But attributes, constructors, methods, roles, and multiple dispatch are ready when a small script grows into a larger project. Python also offers concise classes, especially through dataclasses.

## What Python does better

If you need NumPy, SciPy, pandas, or specialized machine-learning packages, Python may be the obvious choice. It has a much larger user community, library ecosystem, and collection of tutorials. Choosing Raku needn't mean rejecting Python. These are tools, not rival sports teams.

My argument is narrower: **for learning, exploring algorithms, processing text, and writing personal mathematical utilities, Raku can be a particularly enjoyable tool.**

## Try it

Visit [raku.org](https://raku.org/) for installation guidance and [docs.raku.org](https://docs.raku.org/) for the reference documentation. Start with a small question you actually want answered: an average, a unit conversion, an estimate, a table of values. Add error handling and file input only when you need them.

You don't have to want a programming job to benefit from programming. If your main interest is mathematics, engineering, teaching, science, or just understanding the world, a little Raku may help you get more out of your computer.

And for this hunt-and-peck typist, the comfortable syntax is no small bonus.

---

*Next: [Can Raku Make Business Sense?]({% post_url 2026-10-27-can-raku-make-business-sense %}) — Part 2 looks at Raku from an employer's perspective.*
