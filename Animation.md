## Components of the Animation
- **AnimationController:** Manages the animation's state, including the duration and progress.
- **CurvedAnimation:** Adds a curve (in this case, Curves.elasticOut) to the animation, giving it a smooth and more natural feel.
- **ScaleTransition:** Uses the animation to scale the size of the checkmark.

### Initialization
```ruby
late AnimationController _controller;
late Animation<double> _animation;

@override
void initState() {
  super.initState();
  _controller = AnimationController(
    duration: const Duration(seconds: 1),
    vsync: this,
  );

  _animation = CurvedAnimation(
    parent: _controller,
    curve: Curves.elasticOut,
  );

  _controller.forward();
}

```

### AnimationController:
The AnimationController is initialized with a duration of 1 second.
vsync is provided by SingleTickerProviderStateMixin, which helps the animation to be efficient by using a single ticker for the animation.
### CurvedAnimation:
A CurvedAnimation is created to apply the Curves.elasticOut curve to the animation, which makes the checkmark scale in with a slight bounce effect.
### _controller.forward():

This method starts the animation as soon as the widget is initialized.




## Example 
**checkmark popup effect Animation**
```ruby
class CircularCheckmark extends StatelessWidget {
  const CircularCheckmark({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: const Color.fromRGBO(241, 241, 241, 1), 
      body: Center(
        child: AnimatedCheckmark(),
      ),
    );
  }
}

class AnimatedCheckmark extends StatefulWidget {
  @override
  _AnimatedCheckmarkState createState() => _AnimatedCheckmarkState();
}

class _AnimatedCheckmarkState extends State<AnimatedCheckmark>
    with SingleTickerProviderStateMixin {
  late AnimationController _controller;
  late Animation<double> _animation;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: const Duration(seconds: 1),
      vsync: this,
    );

    _animation = CurvedAnimation(
      parent: _controller,
      curve: Curves.elasticOut,
    );

    _controller.forward();
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return ScaleTransition(
      scale: _animation,
      child: Container(
        margin: const EdgeInsets.only(top: 40),
        width: 200,
        height: 200,
        decoration: BoxDecoration(
          color: Colors.blueGrey[50], // Background color for the container
          shape: BoxShape.circle,
        ),
        child: Center(
          child: Container(
            width: 180,
            height: 180,
            decoration: BoxDecoration(
              shape: BoxShape.circle,
              color: Colors.white, // Inner circle color
              border: Border.all(
                color: const Color(0Xff0691A5), // Inner border color
                width: 5, // Inner border width
              ),
            ),
            child: const Center(
              child: Icon(
                Icons.check,
                color: Color(0Xff0691A5), // Checkmark color
                size: 90.0, // Checkmark size
              ),
            ),
          ),
        ),
      ),
    );
  }
}


```

**CircularCheckmark Class**
- CircularCheckmark is a StatelessWidget that returns a Scaffold with a custom background color.
- The body contains a Center widget that centers the AnimatedCheckmark.

## 

**AnimatedCheckmark Class and _AnimatedCheckmarkState**

- AnimatedCheckmark: A StatefulWidget that creates the _AnimatedCheckmarkState.

- _AnimatedCheckmarkState: Uses SingleTickerProviderStateMixin to provide a Ticker for the AnimationController.

- AnimationController: Manages the animation's state and duration (1 second).
- CurvedAnimation: Adds an elasticOut curve to the animation for a bouncing effect.
- _controller.forward(): Starts the animation.
- ScaleTransition: Animates the scaling of its child widget based on the _animation.
##
### Summary
The AnimatedCheckmark widget animates the scaling of a checkmark icon within a circular container using an AnimationController and a CurvedAnimation with an elasticOut curve.
The ScaleTransition widget applies the scaling effect to the child widget based on the animation.
The initState method initializes and starts the animation, and the dispose method ensures the controller is disposed of correctly.






