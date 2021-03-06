# Disallow Unused Labels (no-unused-labels)

Labels that are declared and not used anywhere in the code are most likely an error due to incomplete refactoring.

```js
OUTER_LOOP:
for (const student of students) {
    if (checkScores(student.scores)) {
        continue;
    }
    doSomething(student);
}
```

In this case, probably removing `OUTER_LOOP:` had been forgotten.
Such labels take up space in the code and can lead to confusion by readers.

## Rule Details

This rule is aimed at eliminating unused labels.

The following patterns are considered problems:

```js
/*eslint no-unused-labels: 2*/

A: var foo = 0;  /*error 'A:' is defined but never used.*/

B: {             /*error 'B:' is defined but never used.*/
    foo();
}

C:               /*error 'C:' is defined but never used.*/
for (let i = 0; i < 10; ++i) {
    foo();
}
```

The following patterns are considered not problems:

```js
/*eslint no-unused-labels: 2*/

A: {
    if (foo()) {
        break A;
    }
    bar();
}

B:
for (let i = 0; i < 10; ++i) {
    if (foo()) {
        break B;
    }
    bar();
}
```

## When Not To Use It

If you don't want to be notified about unused labels, then it's safe to disable this rule.

## Related Rules

* [no-extra-label](./no-extra-label.md)
* [no-labels](./no-labels.md)
* [no-label-var](./no-label-var.md)
