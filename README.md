<!-- set up a GitHub Actions workflow to automatically build a JAR file and attach it to a GitHub release when you create one -->
# GitHub Actions

## Run manually

```yaml
on: workflow_dispatch
```

```yaml
on:
  release:
    types: [created]
  workflow_dispatch:
```

## Setup Java Action

Starting from version 2, `actions/setup-java` requires you to specify the `distribution` of Java that you want to use. This is part of the action's setup to allow more flexibility in choosing different Java distributions like Adoptium, Zulu, etc.

```yaml
- name: Set up JDK
  uses: actions/setup-java@v4
  with:
    distribution: 'temurin' # You can choose temurin, zulu, adopt, etc.
    java-version: '11' # Specify the JDK version
```

`temurin` is the successor to AdoptOpenJDK and is provided by the Eclipse Foundation. Adjust the `java-version` to whatever version your project requires.

If you prefer a different distribution, here are a few options you might consider:
- `temurin`: Eclipse Temurin distributions
- `zulu`: Azul Zulu distributions
- `adopt`: AdoptOpenJDK, which is now part of the Eclipse project under the name Temurin

Just replace `'temurin'` with your chosen distribution in the `distribution` field.

<span style="color:blue;font-size:larger;">This project doesn't compile with JDK 21 or 18.  If you use v4 with 1.8 it says it can't find it.</span>

```c
Available versions: 22.0.1+8, 22.0.0+36, 21.0.3+9.0.LTS, 21.0.2+13.0.LTS, 21.0.1+12.0.LTS, 21.0.0+35.0.LTS, 20.0.2+9, 20.0.1+9, 20.0.0+36, 19.0.2+7, 19.0.1+10, 19.0.0+36, 18.0.2+101, 18.0.2+9, 18.0.1+10, 18.0.0+36, 17.0.11+9, 17.0.10+7, 17.0.9+9, 17.0.8+101, 17.0.8+7, 17.0.7+7, 17.0.6+10, 17.0.5+8, 17.0.4+101, 17.0.4+8, 17.0.3+7, 17.0.2+8, 17.0.1+12, 17.0.0+35, etc.
```

This works:

```yaml
- name: Set up JDK
  uses: actions/setup-java@v4
  with:
    distribution: 'temurin'
    java-version: 8.0.302+8
```

<br>
