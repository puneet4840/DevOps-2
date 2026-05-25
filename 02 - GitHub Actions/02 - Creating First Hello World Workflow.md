# Printing Hello World using workflow

Is slide mein hum Hello World workflow create karenge.

Niche diye hue path par ```hello_world.yaml``` file create karlo. Aur yaml code likho.

```
.github/workflow/hello_world.yaml
```

```hello_world.yaml```:
```
name: Hello World Workflow

on:
  workflow_dispatch:

jobs:
  hello_world:
    runs-on: ubuntu-latest

    steps:
      - name: Code Checkout
        uses: actions/checkout@v6.0.2

      - name: Printing Hello World
        run: echo "Hello World"
```

Output:
```
Hello World
```

<br>

### Explanation:

```name: Hello World Workflow```:

Ye workflow ka naam hota hai, matlab pipeline ka naam.

<br>

```
on:
  workflow_dispatch:
```

Agar tum workflow ko manually run karna chate ho, to isse workflow manually run hota hai.

<br>

```
jobs:
  hello_world:
    runs-on: ubuntu-latest
```

Ye hello world job hai, jo ubuntu-latest runner par chal rahi hai.


<br>

```
steps:
      - name: Code Checkout
        uses: actions/checkout@v6.0.2

      - name: Printing Hello World
        run: echo "Hello World"
```

Ye multiple steps tumhari hello_world job ke ander run ho rahe hain.

Step ```- name: Code Checkout``` runner par repo ka code clone karta hai.

Step ```-name: Printing Hello World``` Hello World print kar raha hai.
