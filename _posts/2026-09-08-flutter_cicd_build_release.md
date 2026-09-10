---
layout: post
title: "flutter_cicd_build_release"
date: 2026-09-08 22:27:55 +0000
categories: projects
excerpt: "Flutter Automated CI/CD Release Pipeline I built a production‑ready GitHub Actions workflow that ta..."
---

# Flutter Automated CI/CD Release Pipeline  

I built a **production‑ready GitHub Actions workflow** that takes the pain out of releasing Flutter apps. Every time I push to the `main` branch, the pipeline spins up a fresh Ubuntu runner, compiles a fully optimized release APK, and publishes it as a GitHub Release—all without any manual steps.

## Why I Need This

In mobile development, the release cycle can become a bottleneck. Manually installing dependencies, running the Gradle build, and uploading the resulting APK to a distribution channel wastes time and introduces human error. By automating the whole process:

- **Consistency** – each build runs in an identical environment.  
- **Speed** – a new release appears in seconds after the push lands.  
- **Reliability** – the same commands are executed on every run, eliminating “it works on my machine” issues.  

## How It Works (Step‑by‑Step)

1. **Trigger on Push** – The workflow listens for `push` events on the `main` branch.  
2. **Provision Runner** – GitHub provides an `ubuntu-latest` VM for the job.  
3. **Checkout Code** – The repository source is pulled with `actions/checkout@v5`.  
4. **Setup Java 17** – Android Gradle tools require Java; the workflow installs Azul Zulu’s JDK 17 via `actions/setup-java@v4`.  
5. **Install Flutter** – The latest stable Flutter SDK is fetched using `subosito/flutter-action@v2`.  
6. **Resolve Packages** – `flutter pub get` brings in all dependencies declared in `pubspec.yaml`.  
7. **Build Release APK** – `flutter build apk --release` produces `app-release.apk`.  
8. **Publish GitHub Release** – `softprops/action-gh-release@v2` creates a new release tagged `v<run_number>` (e.g., `v12`) and attaches the APK automatically.

The entire flow is defined in a single YAML file placed at `.github/workflows/main.yml`.

## Key Features I Love

| Feature | What It Gives Me |
|---------|------------------|
| **Automated Triggers** | No manual build steps; every push to `main` kicks off a full CI/CD run. |
| **Java 17 (Zulu) Setup** | Guarantees compatibility with the latest Android tooling. |
| **Flutter Stable Channel** | Always builds with the most recent stable SDK, keeping the app up‑to‑date. |
| **Dependency Resolution** | `flutter pub get` runs automatically, so nothing is missed. |
| **Standalone Release APK** | The generated `app-release.apk` is ready for distribution (Play Store, internal testing, etc.). |
| **Sequential Tagging** | Releases are tagged with the GitHub run number (`v1`, `v2`, …) for clear version tracking. |
| **Zero‑Touch Publishing** | The APK is attached to a GitHub Release without any extra scripting. |

## When to Use This Pipeline

- **Solo or Small Team Projects** – Quickly get a working release pipeline without setting up a full CI/CD server.  
- **Open‑Source Flutter Apps** – Provide downloadable APKs directly from the repository’s Releases page.  
- **Continuous Delivery Environments** – Pair with internal testing tools (Firebase App Distribution, TestFlight via external scripts) for instant feedback.  
- **Learning & Prototyping** – Ideal for newcomers who want to see CI/CD in action without a steep learning curve.

## Getting Started

1. **Add the Workflow**  
   Save the YAML snippet into `.github/workflows/main.yml` in your Flutter project.  

2. **Configure Permissions**  
   In your repo’s **Settings → Actions → General**, set **Workflow permissions** to **Read and write permissions**. This allows the automatically generated `GITHUB_TOKEN` to create releases.  

3. **Push to Main**  
   Once the file is committed, any push to `main` will start the pipeline. Check the **Actions** tab for live logs, and the **Releases** page for the newly uploaded APK.

## Behind the Scenes: The YAML

```yaml
name: Flutter Build APK
on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v5
      - name: Set up Java
        uses: actions/setup-java@v4
        with:
          distribution: "zulu"
          java-version: "17"
      - name: Set up Flutter
        uses: subosito/flutter-action@v2
        with:
          channel: "stable"
      - name: Install dependencies
        run: flutter pub get
      - name: Build production APK
        run: flutter build apk --release
      - name: Create GitHub Release
        uses: softprops/action-gh-release@v2
        with:
          tag_name: v${{ github.run_number }}
          name: Release Build v${{ github.run_number }}
          draft: false
          prerelease: false
          files: build/app/outputs/flutter-apk/app-release.apk
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

The concise steps keep the workflow readable while covering everything needed for a reliable Flutter APK build and distribution pipeline.

## Licensing

The workflow itself is released under the permissive **MIT License**, so feel free to fork, adapt, or embed it in commercial projects. Details are available in the repository’s [LICENSE](LICENSE) file.

---

With this pipeline in place, I can focus on writing Flutter code while GitHub Actions takes care of building and delivering the APKs—exactly the automation any modern mobile developer deserves. Happy coding!