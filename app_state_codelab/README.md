# App State Management Example with Scoped Model

This Flutter project demonstrates **app state management** using the `scoped_model` package. The counter state is shared across the application and managed through a centralized model that notifies listeners of changes.

## Key Features

- ✅ Counter implementation using `scoped_model` package
- ✅ Centralized state management with `CounterModel`
- ✅ Reactive UI updates through `ScopedModelDescendant`
- ✅ Separation of business logic from UI components
- ✅ Both increment and decrement functionality
- ✅ Stateless widgets for better performance

## Dependencies

```yaml
dependencies:
  scoped_model: ^2.0.0
```

## Implementation Details

### State Model

```dart
class CounterModel extends Model {
  int _counter = 0;

  int get counter => _counter;

  void increment() {
    _counter++;
    notifyListeners(); // Notifies all listening widgets
  }

  void decrement() {
    _counter--;
    notifyListeners(); // Triggers UI rebuilds
  }
}
```

### App Structure

```dart
class MyApp extends StatelessWidget {
  final CounterModel model = CounterModel();

  @override
  Widget build(BuildContext context) {
    return ScopedModel<CounterModel>(
      model: model, // Provides model to widget tree
      child: MaterialApp(
        home: CounterWidget(),
      ),
    );
  }
}
```

### Widget Implementation

```dart
class CounterWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ScopedModelDescendant<CounterModel>(
      builder: (context, child, model) => Center(
        child: Column(
          children: <Widget>[
            Text('Counter Value: ${model.counter}'),
            ElevatedButton(
              onPressed: model.increment,
              child: Text('Increment'),
            ),
            ElevatedButton(
              onPressed: model.decrement,
              child: Text('Decrement'),
            ),
          ],
        ),
      ),
    );
  }
}
```

## Architecture Benefits

### Separation of Concerns

- **Model**: Contains business logic and state
- **View**: Handles presentation and user interactions
- **Binding**: `ScopedModelDescendant` connects model to view

### Reactive Updates

- Changes in `CounterModel` automatically trigger UI rebuilds
- Multiple widgets can listen to the same model
- Efficient updates using the observer pattern

### Scalability

- Easy to add new functionality to the model
- Multiple models can be combined for complex state
- Testable business logic separated from UI

## Real-World Applications

This pattern scales well for:

- **User Authentication**: Login state, user profiles, permissions
- **Shopping Carts**: Items, quantities, totals, checkout state
- **App Settings**: Theme, language, notifications preferences
- **Data Management**: API responses, caching, offline state

## Testing

With scoped model, you can easily unit test your business logic:

```dart
void main() {
  group('CounterModel', () {
    test('should increment counter', () {
      final model = CounterModel();
      model.increment();
      expect(model.counter, 1);
    });

    test('should decrement counter', () {
      final model = CounterModel();
      model.increment();
      model.decrement();
      expect(model.counter, 0);
    });
  });
}
```

## Running the Project

```bash
cd app_state_codelab
flutter pub get
flutter run
```

## Evolution to Modern State Management

While `scoped_model` is demonstrated here, consider these modern alternatives:

- **Provider**: Google's recommended successor to scoped_model
- **Riverpod**: Compile-time safe, more powerful Provider
- **BLoC/Cubit**: Event-driven architecture with streams
- **GetX**: Simple reactive state management

## Comparison

Compare this implementation with the `ephemeral_state_codelab` project to understand when to use app-wide state management versus local widget state. See the main project README for a comprehensive comparison and best practices guide.
