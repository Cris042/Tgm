# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Tllm is a minimal Maven Java project (IntelliJ IDEA scaffold) targeting **Java 25**. It currently contains a single class, `org.example.Main`, and uses Java 25 language features: a compact `static void main()` (no `String[] args`) and `java.lang.IO.println` (JEP 512), so a JDK 25+ is required to compile or run.

## Environment & Commands

- The repo lives on a Windows filesystem but is worked on from WSL. In WSL, JDK 25 (Corretto, via SDKMAN) is available, but **`mvn` is not on the PATH and there is no Maven wrapper** — the project is normally built/run from IntelliJ on Windows.
- Run directly with the JDK (works without Maven, using single-file source launch):
  ```
  java src/main/java/org/example/Main.java
  ```
- If Maven is available: `mvn compile` to build. There is no exec or test framework configured — the pom declares no dependencies or plugins, only compiler source/target 25.
- No tests exist yet (`src/test/java` is empty). Adding tests requires first adding a test dependency (e.g., JUnit) to `pom.xml`.
