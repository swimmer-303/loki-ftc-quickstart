# NextFTC + PedroPathing Quickstart

A comprehensive FTC robotics quickstart template featuring NextFTC command-based programming and PedroPathing autonomous navigation.

## 🚀 Features

- **NextFTC 0.6.1**: Modern command-based programming framework
- **PedroPathing 1.0.9**: Advanced path following and autonomous navigation
- **FTC SDK 10.2.0**: Latest official FTC Software Development Kit
- **Dual Language Support**: Java and Kotlin examples
- **Ready-to-Use Examples**: Claw, Lift, and Autonomous implementations

## 📋 Prerequisites

- **Android Studio Ladybug (2024.2)** or later
- **Java 8** or later
- **Git** for version control
- **FTC Robot Controller** device (Control Hub or Android phone)

## 🛠️ Quick Setup

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/loki-ftc-quickstart.git
cd loki-ftc-quickstart
```

### 2. Open in Android Studio
1. Launch Android Studio
2. Select "Open an existing Android Studio project"
3. Navigate to the cloned repository folder
4. Click "OK" and wait for Gradle sync

### 3. Configure Your Robot
1. Connect your Robot Controller device
2. Build and deploy the app: `Build > Make Project`
3. Install the APK on your device

## 📁 Project Structure

```
loki-ftc-quickstart/
├── TeamCode/src/main/java/org/firstinspires/ftc/teamcode/
│   ├── example/
│   │   ├── java/           # Java examples
│   │   │   ├── AutonomousProgram.java
│   │   │   ├── Claw.java
│   │   │   └── Lift.java
│   │   └── kotlin/         # Kotlin examples
│   │       ├── AutonomousProgram.kt
│   │       ├── Claw.kt
│   │       └── Lift.kt
│   └── pedroPathing/       # PedroPathing integration
│       ├── constants/
│       ├── examples/
│       └── tuners_tests/
├── FtcRobotController/     # Core FTC SDK
└── build files...
```

## 🎯 Getting Started

### NextFTC Command-Based Programming

NextFTC provides a modern, WPILib-inspired command-based framework for FTC:

```java
// Example Subsystem (Claw.java)
public class Claw extends Subsystem {
    public static final Claw INSTANCE = new Claw();
    private Servo servo;

    public Command open() {
        return new ServoToPosition(servo, 0.9, this);
    }

    public Command close() {
        return new ServoToPosition(servo, 0.2, this);
    }
}

// Example OpMode
@Autonomous(name = "My Autonomous")
public class MyAutonomous extends NextFTCOpMode {
    public MyAutonomous() {
        super(Claw.INSTANCE, Lift.INSTANCE);
    }

    @Override
    public void onStartButtonPressed() {
        new SequentialGroup(
            Claw.INSTANCE.close(),
            Lift.INSTANCE.toHigh(),
            Claw.INSTANCE.open()
        ).invoke();
    }
}
```

### PedroPathing Autonomous Navigation

PedroPathing provides advanced path following capabilities:

```java
// Configure your follower
Follower follower = new Follower(hardwareMap);

// Create and follow paths
Path path = new Path(new BezierLine(
    new Point(0, 0, Point.CARTESIAN),
    new Point(24, 24, Point.CARTESIAN)
));

follower.followPath(path);
```

## 📚 Documentation Links

- **NextFTC Documentation**: [docs.rowanmcalpin.com](https://docs.rowanmcalpin.com/)
- **PedroPathing Documentation**: [pedropathing.com](https://pedropathing.com/)
- **FTC Documentation**: [ftc-docs.firstinspires.org](https://ftc-docs.firstinspires.org/)

## 🤝 Community & Support

- **NextFTC Discord**: [discord.gg/PjP9Ze6fkX](https://discord.gg/PjP9Ze6fkX)
- **PedroPathing Discord**: [discord.gg/2GfC4qBP5s](https://discord.gg/2GfC4qBP5s)
- **FTC Community**: [ftc-community.firstinspires.org](https://ftc-community.firstinspires.org/)

## 🔧 Development Workflow

### Building the Project
```bash
./gradlew build
```

### Running Tests
```bash
./gradlew test
```

### Code Formatting
This project uses standard Java/Kotlin formatting. Configure your IDE to use:
- **Indent**: 4 spaces
- **Line Length**: 120 characters
- **Import Organization**: Automatic

## 📦 Dependencies

| Library | Version | Purpose |
|---------|---------|---------|
| FTC SDK | 10.2.0 | Core FTC framework |
| NextFTC Core | 0.6.1 | Command-based programming |
| NextFTC FTC | 0.6.1 | FTC-specific implementations |
| NextFTC Pedro | 0.6.1 | PedroPathing integration |
| PedroPathing | 1.0.9 | Path following and navigation |
| FTC Dashboard | 0.4.16 | Real-time debugging |

## 🚨 Troubleshooting

### Common Issues

**Build Errors:**
- Ensure you're using Android Studio Ladybug (2024.2) or later
- Check that all dependencies are properly downloaded
- Try `Build > Clean Project` then `Build > Rebuild Project`

**Device Connection Issues:**
- Enable Developer Options and USB Debugging on your device
- Install the correct USB drivers for your device
- Check that the device is properly configured in the FTC app

**Runtime Errors:**
- Check the Robot Controller logs in `/sdcard/FIRST/logs/`
- Verify hardware configuration matches your code
- Ensure all required permissions are granted

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m 'Add amazing feature'`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **NextFTC Team** for the excellent command-based framework
- **PedroPathing Team** for advanced autonomous capabilities
- **FIRST Tech Challenge** for the robotics platform
- **FTC Community** for continuous support and innovation

---

**Happy Coding! 🤖**
