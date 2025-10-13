# Contributing to RANTAI AgroViz

First off, thank you for considering contributing to RANTAI AgroViz! 🌱

We welcome contributions from developers, farmers, agricultural experts, and anyone passionate about improving agriculture through technology.

## 🎯 Code of Conduct

By participating in this project, you agree to:
- Be respectful and inclusive
- Focus on constructive feedback
- Help others learn and grow
- Prioritize the needs of farmers and agricultural communities

## 🚀 How Can I Contribute?

### 1. Reporting Bugs

Before creating bug reports, please check existing issues to avoid duplicates.

**Good bug reports include:**
- Clear, descriptive title
- Steps to reproduce the issue
- Expected behavior vs actual behavior
- Screenshots (if applicable)
- Environment details (browser, OS, etc.)

**Example:**
```
Title: Weather alerts not showing for Jakarta

Steps to reproduce:
1. Select Jakarta as location
2. Wait for weather data to load
3. Check weather alerts section

Expected: Should show weather alerts if conditions are critical
Actual: No alerts displayed despite heavy rain forecast

Environment: Chrome 120, Windows 11
```

### 2. Suggesting Features

We love feature ideas! Please provide:
- Clear description of the feature
- Problem it solves for farmers
- How it should work (user flow)
- Priority level (nice-to-have vs critical)

**Example:**
```
Feature: SMS Weather Alerts

Problem: Many farmers don't have constant internet access
Solution: Send critical weather alerts via SMS
User Flow: Farmer registers phone number → System sends SMS for critical alerts
Priority: High (accessibility for rural farmers)
```

### 3. Code Contributions

#### Setup Development Environment

```bash
# Fork and clone the repo
git clone https://github.com/YOUR_USERNAME/rantai-agroviz.git
cd rantai-agroviz

# Install dependencies
npm install

# Run development server
npm run dev
```

#### Code Style Guidelines

**TypeScript:**
- Use strict TypeScript with explicit types
- Avoid `any` type (use `unknown` if necessary)
- Prefer interfaces over types for object shapes
- Use meaningful variable names

```typescript
// ❌ Bad
const d = (a: any) => a.map((x: any) => x * 2);

// ✅ Good
const doubleNumbers = (numbers: number[]): number[] => {
  return numbers.map((num: number) => num * 2);
};
```

**React Components:**
- Use functional components with hooks
- Keep components small and focused
- Extract reusable logic into custom hooks
- Use proper prop types

```typescript
// ✅ Good component structure
interface WeatherCardProps {
  temperature: number;
  location: string;
  onRefresh: () => void;
}

export function WeatherCard({ temperature, location, onRefresh }: WeatherCardProps) {
  return (
    <Card>
      <CardHeader>
        <CardTitle>{location}</CardTitle>
      </CardHeader>
      <CardContent>
        <p>{temperature}°C</p>
        <Button onClick={onRefresh}>Refresh</Button>
      </CardContent>
    </Card>
  );
}
```

**Styling:**
- Use Tailwind CSS utility classes
- Follow existing color scheme (cyberpunk theme)
- Ensure mobile responsiveness
- Use shadcn/ui components when possible

**File Organization:**
```
src/
├── components/       # React components
├── lib/             # Utility functions, services
├── hooks/           # Custom React hooks
├── types/           # TypeScript type definitions
└── app/             # Next.js app router pages
```

#### Commit Messages

Follow conventional commits format:

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting)
- `refactor`: Code refactoring
- `test`: Adding/updating tests
- `chore`: Build process, dependencies

**Examples:**
```
feat(weather): add hourly forecast display

- Added hourly temperature and rainfall chart
- Implemented 24-hour forecast view
- Updated WeatherService to fetch hourly data

Closes #45

---

fix(dao): voting button not responding on mobile

- Fixed touch event handler for voting buttons
- Added proper loading states
- Improved mobile button sizing

Fixes #78
```

#### Pull Request Process

1. **Create a feature branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```

2. **Make your changes**
   - Write clean, documented code
   - Add tests if applicable
   - Update documentation

3. **Test thoroughly**
   ```bash
   npm run build  # Ensure it builds
   npm run lint   # Check for linting errors
   ```

4. **Commit your changes**
   ```bash
   git commit -m "feat(feature): add amazing feature"
   ```

5. **Push to your fork**
   ```bash
   git push origin feature/amazing-feature
   ```

6. **Open Pull Request**
   - Use clear, descriptive title
   - Reference related issues
   - Describe what changed and why
   - Add screenshots for UI changes
   - Ensure CI passes

**PR Template:**
```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Testing
How did you test this?

## Screenshots
(if applicable)

## Related Issues
Closes #123
```

## 🌾 Agricultural Domain Contributions

Have farming expertise? We need you!

### Areas Where Farmers Can Contribute:
- **Validate fuzzy logic rules** - Are AI recommendations accurate?
- **Suggest crop types** - What crops should we support?
- **Review weather alerts** - Are thresholds realistic?
- **Test with real data** - Use the app on your farm!
- **Translate content** - Help with local language support
- **Share use cases** - What features would help you most?

### Domain Expert Contributions:
- Agronomist? Help validate decision support algorithms
- Supply chain expert? Review blockchain tracking flow
- Financial expert? Suggest lending/insurance features
- IoT engineer? Help with sensor integration specs

## 🔧 Areas Needing Contributions

### High Priority
- [ ] Connect SpacetimeDB to all components (data persistence)
- [ ] Real commodity price API integration
- [ ] Wallet-based authentication system
- [ ] Mobile app version (React Native)
- [ ] Offline mode with data sync

### Medium Priority
- [ ] Computer vision disease detection
- [ ] IoT sensor integration (MQTT protocol)
- [ ] Multi-language support (Bahasa Indonesia)
- [ ] Export reports (PDF/CSV)
- [ ] Advanced analytics dashboard

### Nice to Have
- [ ] Satellite imagery overlay
- [ ] Drone integration
- [ ] Voice command support
- [ ] WhatsApp bot integration
- [ ] Gamification for learning

## 📚 Resources

**Learn the Tech Stack:**
- [Next.js Documentation](https://nextjs.org/docs)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/)
- [Tailwind CSS](https://tailwindcss.com/docs)
- [SpacetimeDB Docs](https://spacetimedb.com/docs)
- [OnchainKit Guide](https://onchainkit.xyz)

**Agricultural Resources:**
- [FAO Agricultural Data](http://www.fao.org/faostat/)
- [Weather API Documentation](https://www.weatherapi.com/docs/)
- [IoT for Agriculture](https://www.iot-for-all.com/iot-in-agriculture/)

## 🤝 Community

- **GitHub Discussions**: Ask questions, share ideas
- **Issues**: Report bugs, request features
- **Pull Requests**: Contribute code
- **Email**: support@rantai.elpeef.com

## 🎓 Mentorship

New to open source? We're happy to help!
- Label `good first issue` for beginners
- Maintainers available for guidance
- Pair programming sessions available

## 🏆 Recognition

Contributors will be:
- Listed in README.md
- Mentioned in release notes
- Eligible for future bounties/grants
- Part of agricultural tech revolution!

---

**Thank you for helping farmers with technology!** 🌱

Every contribution, no matter how small, makes a difference in improving agriculture and food security.

Happy coding! 🚀
