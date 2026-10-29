# Extending the Library

The library is designed to be easily extendable. <br> 
You can add your own actions and overrides.

## Adding your own actions

To add your own actions, you need to create a class that extends the `DialogueAction` class.<br>
Then you need to register your action in the `DialogueManager`.<br>

### Example of a custom action that prints a message to the console when executed.

This is a simple example of a custom action that prints a message to the console when executed.<br>
For more complex actions, check what methods are available in the `DialogueAction` class.

```java
public class MyCustomAction extends DialogueAction {

    public static final StreamCodec<RegistryFriendlyByteBuf, DialogueMessage> CUSTOM_ACTION_STREAM_CODEC = StreamCodec.composite(
        ByteBufCodecs.STRING_UTF8, MyCustomAction::getMessage,
        MyCustomAction::new
    );

    private static final DialogueManager.DialogueActionType<MyCustomAction> TYPE = DialogueManager.registerActionType(
        ResourceLocation.fromNamespaceAndPath("my_mod", "my_custom_action"), CUSTOM_ACTION_STREAM_CODEC
    );

    private String message = "Hello, this is my custom action!";

    // Constructor for network deserialization
    public MyCustomAction(String message) {
        this.message = message;
    }
    
    // Constructor for json deserialization
    public MyCustomAction(JsonObject json) {
        if(json.has("message"))
            this.message = json.get("message").getAsString();
    }

    // This code is executed when the action is executed in a dialogue.
    @Override
    public void setup(DialogueScreen screen) {
        System.out.println("My custom action executed!\nMy message: " + message);
    }

    // For network serialization
    public String getMessage() {
        return message;
    }

    @Override
    public DialogueManager.DialogueActionType<?> getType() { return TYPE; }
}
```

Then you need to register your action in the `DialogueManager`.<br>
Somewhere in your mod initialization code, you can register your action like this:

```java
// Initialization code...

DialogueManager.registerCustomAction(ResourceLocation.fromNamespaceAndPath("my_mod", "my_custom_action"), MyCustomAction.class);
```

## Overriding existing actions

!!! warning "Experimental"
    
    This feature is experimental and may change in the future.

To override an existing action, you need to create a new class that extends the existing action class and override the methods you want to change. <br>
Then register your overrides in the `DialogueManager`.<br>

When registering an override, you must specify the namespace of the override.<br>
This will determine if the override will be used for a certain dialogue.<br>

For example, if you register an override with the namespace `my_mod`, it will only be used for dialogues that are in the `my_mod` namespace.<br>

```java
DialogueManager.registerOverload("my_mod", "message", MyCustomMessageOverride.class);
```