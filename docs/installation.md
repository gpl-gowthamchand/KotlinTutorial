# Kotlin Installation Guide

This guide will help you install Kotlin on your system, regardless of your operating system.

## Prerequisites

Before installing Kotlin, you'll need:
- **Java Development Kit (JDK)** version 8 or higher
- **An IDE** (IntelliJ IDEA, Android Studio, or VS Code)

## Installing Java (JDK)

### Windows
1. Download OpenJDK from [Adoptium](https://adoptium.net/)
2. Run the installer and follow the setup wizard
3. Add Java to your PATH environment variable
4. Verify installation: `java -version`

### macOS
1. Install Homebrew if you haven't: `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
2. Install OpenJDK: `brew install openjdk`
3. Link the JDK: `sudo ln -sfn /opt/homebrew/opt/openjdk/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk.jdk`
4. Verify installation: `java -version`

### Linux (Ubuntu/Debian)
1. Update package list: `sudo apt update`
2. Install OpenJDK: `sudo apt install openjdk-11-jdk`
3. Verify installation: `java -version`

## Installing Kotlin

### Option 1: Using SDKMAN! (Recommended for Linux/macOS)
1. Install SDKMAN!: `curl -s "https://get.sdkman.io" | bash`
2. Restart your terminal or run: `source "$HOME/.sdkman/bin/sdkman-init.sh"`
3. Install Kotlin: `sdk install kotlin`
4. Verify installation: `kotlin -version`

### Option 2: Using Homebrew (macOS)
1. Install Kotlin: `brew install kotlin`
2. Verify installation: `kotlin -version`

### Option 3: Manual Installation
1. Download the latest Kotlin compiler from [GitHub Releases](https://github.com/JetBrains/kotlin/releases)
2. Extract the archive to a directory (e.g., `/usr/local/kotlin`)
3. Add the `bin` directory to your PATH
4. Verify installation: `kotlin -version`

## Installing an IDE

### IntelliJ IDEA (Recommended)
1. Download [IntelliJ IDEA Community Edition](https://www.jetbrains.com/idea/download/)
2. Install and launch the IDE
3. Install the Kotlin plugin (usually pre-installed)
4. Create a new Kotlin project

### Android Studio
1. Download [Android Studio](https://developer.android.com/studio)
2. Install and launch the IDE
3. Kotlin support is included by default
4. Create a new Android project with Kotlin

### VS Code
1. Download [VS Code](https://code.visualstudio.com/)
2. Install the Kotlin extension by fwcd
3. Install the Kotlin Language Server

## Creating Your First Kotlin Project

### Using IntelliJ IDEA
1. File → New → Project
2. Select "Kotlin" → "JVM | IDEA"
3. Choose project name and location
4. Click "Create"
5. Right-click on `src` → New → Kotlin File/Class
6. Name it `Main.kt`
7. Add this code:
```kotlin
fun main() {
    println("Hello, Kotlin!")
}
```
8. Run the program (Shift + F10)

### Using Command Line
1. Create a new directory: `mkdir my-kotlin-project`
2. Navigate to it: `cd my-kotlin-project`
3. Create `Main.kt`:
```kotlin
fun main() {
    println("Hello, Kotlin!")
}
```
4. Compile: `kotlinc Main.kt -include-runtime -d Main.jar`
5. Run: `java -jar Main.jar`

## Verifying Your Setup

Run these commands to ensure everything is working:

```bash
# Check Java version
java -version

# Check Kotlin version
kotlin -version

# Check if you can compile and run Kotlin
echo 'fun main() { println("Hello, Kotlin!") }' > test.kt
kotlinc test.kt -include-runtime -d test.jar
java -jar test.jar
```

## Troubleshooting

### Common Issues

**"kotlin: command not found"**
- Ensure Kotlin is in your PATH
- Restart your terminal after installation

**"Java not found"**
- Install JDK first
- Set JAVA_HOME environment variable

**Permission denied errors**
- Use `sudo` for system-wide installations
- Check file permissions

### Getting Help

- [Kotlin Official Documentation](https://kotlinlang.org/docs/home.html)
- [Kotlin GitHub Issues](https://github.com/JetBrains/kotlin/issues)
- [Kotlin Community Slack](https://kotlinlang.slack.com/)

## Next Steps

Once you have Kotlin installed, you can:
1. [Start with Hello World](basics/01-hello-world.md)
2. [Learn about Variables and Data Types](basics/02-variables-data-types.md)
3. [Explore Control Flow](control-flow/01-if-expressions.md)

Happy coding with Kotlin! 🚀
