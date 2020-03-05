# Services

Starting android Oreo , we cannot keep a normal service running while our app is or goes to the background.

## Foreground

Foreground service allow our app to run a service without being killed by the system if the app or activity goes to the background.

---

### How to start a service as a foreground service?

**If the app or activity that starts the service is in the foreground, we have to :**

1. create the explicit intent.
1. call startService(intent);
1. inside onStartCommand() -> call startForeground(int,Notification);

**If the app or activity that starts the service is in the background, we have to:**

1. create the explicit intent.
2. call startForegroundService(intent);
3. inside onStartCommand()-> call startForeground(int,Notification); within 5 seconds otherwise the system will stop the service.

START_STICKY, will let the system to recreate the service if it gets killed by the sys but by passing null to the intent.

### onStartCommand vs onCreate:

**onStartCommand** is called every time we call startService.
**onCreate** is called only once when the service is being created.

### How to stop a foreground service:

We can stop a service either from outside or inside the service class.
Inside the class we call : stopSelf().
Outside the class we call : stopService(intent) , by passing the intent of the service.
Both methods will destroy the service, so if we call startService again, **onCreate** of the service will be called.
