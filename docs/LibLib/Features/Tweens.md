# Tweens

Tweens are a way to animate values over time.<br>
They can be used to animate any value with a corresponding interpolator, such as `float`, `double`, `integer`, `Vec2`, `Vec3`, `Vector3f`, rotations (stored in a `Vector3f`) and `Color`.<br>

Tweens are stored in a `TweenSequence`, and are executed in order.<br>
Each Sequence has a specific side, either `Client` or `Server`, and will only be executed on that side.<br>
Client Tweens are much smoother than Server Tweens, and should be used for any visual effect.<br>
Server Tweens should be used for any logic that needs to be executed on the server, such as moving entities.<br>

## Using TweenSequences

To create a `TweenSequence`, you need to call `TweenManager.createTweenSequence(TweenManager.TweenSide.CLIENT)` or `TweenManager.createTweenSequence(TweenManager.TweenSide.SERVER)` method.<br>
This method will return a `TweenSequence` object, which you can use to add tweens to the sequence.<br>

There are multiple Tweens avaiable, such as `TweenProperty`, `TweenWait`, `TweenCallback`, and `TweenParallel`.<br>

You can add these like this : <br>

```java
TweenSequence sequence = TweenManager.createTweenSequence(TweenManager.TweenSide.CLIENT);

sequence.setParallel(true); //set the next tweens up until another sequence.setParallel() to be executed in parralel.
TweenProperty propertyTween = sequence.tweenProperty(myObject::getMyProperty, myObject::setMyProperty, Interpolator.FLOAT)
    .values(0.0f, 1.0f)
    .duration(20) //duration in ticks
    .easing(Easing.SINE_IN_OUT);

TweenWait waitTween = sequence.tweenWait(20); //wait for 20 ticks
sequence.setParallel(false);

TweenCallback callbackTween = sequence.tweenCallback(() -> {
    System.out.println("Callback executed!");
});

sequence.play();
```

If you set the sequence to be parallel, all tweens added after that will be executed in parallel until you set it back to sequential with `sequence.setParallel(false)`.<br>
This means that the `TweenProperty` and `TweenWait` will be executed in parallel but the `TweenCallback` will be executed after them.<br>