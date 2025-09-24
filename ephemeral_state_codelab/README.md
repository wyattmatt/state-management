# Ephemeral State Management Example

This Flutter project demonstrates **ephemeral state management** using `StatefulWidget` and `setState()`. The counter state is contained within a single widget and doesn't persist across navigation or widget rebuilds.

## Key Features

- ✅ Simple counter implementation using local state
- ✅ State managed within `_CounterWidgetState`
- ✅ Direct UI updates using `setState()`
- ✅ No external dependencies required
- ✅ Minimal boilerplate code

## Implementation Details

### State Management

```dart
class _CounterWidgetState extends State<CounterWidget> {
  int _counter = 0; // Local ephemeral state

  @override
  Widget build(BuildContext context) {
    return Center(
      child: Column(
        children: <Widget>[
          Text('Counter Value: $_counter'),
          ElevatedButton(
            onPressed: () {
              setState(() {
                _counter++; // Triggers widget rebuild
              });
            },
            child: Text('Increment'),
          ),
        ],
      ),
    );
  }
}
```

### Characteristics

- **Scope**: Limited to the `CounterWidget` only
- **Persistence**: State is lost when widget is disposed
- **Sharing**: Cannot be accessed by other widgets
- **Performance**: Direct, efficient updates
- **Complexity**: Simple and easy to understand

## When to Use Ephemeral State

This pattern is ideal for:

- Form field values and validation states
- Animation controllers and progress
- Currently selected tabs or menu items
- Scroll positions and view states
- Any UI state that doesn't need to be shared

## Running the Project

```bash
cd ephemeral_state_codelab
flutter pub get
flutter run
```

## Comparison

Compare this implementation with the `app_state_codelab` project to understand the differences between ephemeral and app state management approaches. See the main project README for a detailed comparison.
