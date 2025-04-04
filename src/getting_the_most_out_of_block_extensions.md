# Getting the most out of block extensions

Have everything in a faction as interconnected by using block extensions. If you have a good plan of what you are making, it will save you time.

Below is how you might want to map out an extension hierachy. The example has 3 types of hull, each containing squares and triangles, both of which have 4 scales, plus some non-hull components. Every branch represents an `extends` field. This is how I manage my mods.
```
Original Hull Square
├── Scale 2
├── Scale 3
├── Scale 4
│
├── Hull Triangle
│   ├── Scale 2
│   ├──	Scale 3
│   └──	Scale 4
│
│
├── Differently Colored Hull Square
│   ├──	Scale 2
│   ├──	Scale 3
│   ├──	Scale 4
│   └──	Differently Colored Hull Triangle
│	    ├── Scale 2
│	    ├── Scale 3
│	    └── Scale 4
│
│
├── Armored Hull Square
│   ├──	Scale 2
│   ├──	Scale 3
│   ├──	Scale 4
│   └──	Armored Hull Triangle
│	    ├── Scale 2
│	    ├── Scale 3
│	    └── Scale 4
│
│
├── Command
│
├── Generator Scale 1
│   ├── Generator Scale 2
│   ├── Generator Scale 3
│   └── Generator Scale 4
│
├── Gun Scale 1
│   ├── Gun Scale 2
│   └── Gun Scale 3
│
└── Different Type of Gun Scale 1
    ├── Different Type of Gun Scale 2
    └── Different Type of Gun Scale 3

```
I like making the most of block extension but I keep different components seperate to not sacrifice my ability to create and edit stuff.

For example, I like seperating different guns in the extends tree. This makes them easier to work with as they do not depend on each other for features.
