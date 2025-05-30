# Contributing to Loki FTC Quickstart

Thank you for your interest in contributing to our FTC robotics project! This guide will help you get started with contributing code, reporting issues, and improving our robot's capabilities.

## 🚀 Getting Started

### Prerequisites

Before you begin, ensure you have the following installed:

- **Android Studio** (latest stable version)
- **Git** for version control
- **Java Development Kit (JDK) 17** or later
- **FTC Robot Controller app** on your robot's phone

### Setting Up Your Development Environment

1. **Fork and Clone the Repository**
   ```bash
   git clone https://github.com/your-username/loki-ftc-quickstart.git
   cd loki-ftc-quickstart
   ```

2. **Open in Android Studio**
   - Launch Android Studio
   - Select "Open an existing Android Studio project"
   - Navigate to the cloned repository folder
   - Wait for Gradle sync to complete

3. **Verify Setup**
   ```bash
   ./gradlew build
   ```

## 📋 Development Workflow

### Branch Strategy

We use a simplified Git flow:

- **`main`** - Production-ready code, always deployable
- **`develop`** - Integration branch for features
- **`feature/feature-name`** - Individual feature development
- **`hotfix/issue-description`** - Critical bug fixes

### Creating a New Feature

1. **Create a Feature Branch**
   ```bash
   git checkout develop
   git pull origin develop
   git checkout -b feature/your-feature-name
   ```

2. **Make Your Changes**
   - Write clean, well-documented code
   - Follow our coding standards (see below)
   - Add tests for new functionality

3. **Test Your Changes**
   ```bash
   # Run all tests
   ./gradlew test
   
   # Run code quality checks
   ./gradlew checkAll
   
   # Format code
   ./gradlew formatAll
   ```

4. **Commit Your Changes**
   ```bash
   git add .
   git commit -m "feat: add new autonomous path for scoring"
   ```

5. **Push and Create Pull Request**
   ```bash
   git push origin feature/your-feature-name
   ```
   Then create a pull request on GitHub targeting the `develop` branch.

## 📝 Coding Standards

### Java Code Style

- **Indentation**: 4 spaces (no tabs)
- **Line Length**: Maximum 120 characters
- **Naming Conventions**:
  - Classes: `PascalCase` (e.g., `ClawSubsystem`)
  - Methods: `camelCase` (e.g., `openClaw()`)
  - Constants: `UPPER_SNAKE_CASE` (e.g., `MAX_SPEED`)
  - Variables: `camelCase` (e.g., `motorPower`)

### Kotlin Code Style

- Follow the same conventions as Java
- Use Kotlin idioms where appropriate
- Prefer `val` over `var` when possible
- Use data classes for simple data containers

### Documentation

- **Classes**: Document purpose and usage
- **Public Methods**: Include JavaDoc/KDoc with parameters and return values
- **Complex Logic**: Add inline comments explaining the "why"

Example:
```java
/**
 * Controls the robot's claw mechanism for picking up and releasing game elements.
 * 
 * @author Team Loki
 */
public class ClawSubsystem extends SubsystemBase {
    
    /**
     * Opens the claw to release the current game element.
     * 
     * @param speed The speed at which to open (0.0 to 1.0)
     */
    public void openClaw(double speed) {
        // Implementation here
    }
}
```

## 🧪 Testing Guidelines

### Unit Tests

- Write tests for all public methods
- Use descriptive test names: `shouldOpenClawWhenCommandExecuted()`
- Test both success and failure scenarios
- Mock external dependencies

### Integration Tests

- Test subsystem interactions
- Verify autonomous routines work correctly
- Test hardware integration (when possible)

### Example Test Structure

```java
@Test
public void shouldMoveToTargetPositionWhenCommandExecuted() {
    // Arrange
    ClawSubsystem claw = new ClawSubsystem();
    double targetPosition = 0.5;
    
    // Act
    claw.setPosition(targetPosition);
    
    // Assert
    assertEquals(targetPosition, claw.getPosition(), 0.01);
}
```

## 🔧 Code Quality Tools

We use several tools to maintain code quality:

### Spotless (Code Formatting)
```bash
# Check formatting
./gradlew spotlessCheck

# Apply formatting
./gradlew spotlessApply
```

### Detekt (Kotlin Static Analysis)
```bash
# Run static analysis
./gradlew detekt
```

### Dependency Vulnerability Scanning
```bash
# Check for vulnerable dependencies
./gradlew dependencyCheckAnalyze
```

## 🤖 FTC-Specific Guidelines

### OpMode Development

1. **Naming Convention**: Use descriptive names
   - Autonomous: `RedLeftAutonomous`, `BlueRightAutonomous`
   - TeleOp: `MainTeleOp`, `TestTeleOp`

2. **Structure**: Keep OpModes simple, delegate to subsystems
   ```java
   @Autonomous(name = "Red Left Autonomous")
   public class RedLeftAutonomous extends CommandOpMode {
       @Override
       public void initialize() {
           // Initialize subsystems and commands
       }
   }
   ```

3. **Hardware Configuration**: Use consistent naming
   - Motors: `leftDrive`, `rightDrive`, `clawMotor`
   - Servos: `clawServo`, `wristServo`
   - Sensors: `colorSensor`, `distanceSensor`

### Autonomous Programming

1. **Use PedroPathing** for path following
2. **Modular Commands**: Break complex actions into smaller commands
3. **Error Handling**: Always include timeout and error conditions
4. **Testing**: Test autonomous routines extensively

### TeleOp Programming

1. **Responsive Controls**: Ensure controls feel natural
2. **Safety Features**: Include emergency stops and limits
3. **Driver Feedback**: Provide telemetry and gamepad rumble
4. **Customization**: Allow drivers to adjust sensitivity

## 📊 Performance Guidelines

### Optimization Tips

1. **Loop Time**: Keep loop times under 20ms
2. **Memory Usage**: Avoid creating objects in loops
3. **Sensor Reading**: Cache sensor values when possible
4. **Motor Updates**: Only update motors when values change

### Telemetry Best Practices

```java
// Good: Organized and informative
telemetry.addData("Drive", "Left: %.2f, Right: %.2f", leftPower, rightPower);
telemetry.addData("Claw", "Position: %.2f", clawPosition);
telemetry.addData("Sensors", "Distance: %.1f cm", distance);
telemetry.update();
```

## 🐛 Issue Reporting

When reporting bugs or requesting features:

1. **Use GitHub Issues** with appropriate labels
2. **Provide Context**: Include steps to reproduce
3. **Include Logs**: Attach relevant error messages
4. **Hardware Info**: Specify robot configuration if relevant

### Issue Template

```markdown
**Description**: Brief description of the issue

**Steps to Reproduce**:
1. Step one
2. Step two
3. Step three

**Expected Behavior**: What should happen

**Actual Behavior**: What actually happens

**Environment**:
- FTC SDK Version: 
- Android Version:
- Robot Configuration:
```

## 🎯 Pull Request Guidelines

### Before Submitting

- [ ] Code follows style guidelines
- [ ] Tests pass locally
- [ ] Code quality checks pass
- [ ] Documentation is updated
- [ ] Commit messages are descriptive

### Pull Request Template

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Testing
- [ ] Unit tests added/updated
- [ ] Integration tests pass
- [ ] Tested on robot hardware

## Checklist
- [ ] Code follows style guidelines
- [ ] Self-review completed
- [ ] Documentation updated
- [ ] No merge conflicts
```

## 🏆 Recognition

Contributors will be recognized in:
- README.md contributors section
- Git commit history
- Team presentations and documentation

## 📞 Getting Help

- **Discord**: Join our team Discord for real-time help
- **GitHub Discussions**: For longer-form questions
- **Mentors**: Reach out to team mentors for guidance
- **FTC Community**: Utilize FTC Discord and forums

## 📚 Additional Resources

- [FTC Programming Resources](https://ftc-docs.firstinspires.org/)
- [NextFTC Documentation](https://github.com/Dairy-Foundation/NextFTC)
- [PedroPathing Guide](https://github.com/pedropathing/PedroPathing)
- [Android Studio Tips](https://developer.android.com/studio/intro)

---

Thank you for contributing to our FTC robotics journey! Every contribution, no matter how small, helps make our robot better and our team stronger. 🤖✨ 