# 02-DebugBlockbreaker-cdoll

In diesem Spiel kann, ist es das Ziel, die schwebenden Bloecke in der Luft zu zerstören. Die blocke zerstören sich, wenn der Ball einmal ankommt. Der Ball reflektiert an Wand und Decke. Man hat einen kleinen waagerechten Boden und kan diesen über dem sonst offenen Boden hin- und her schieben um zu verhindern, dass der Ball runterfällt. Wenn der Ball runterfällt hat man verloren und es gibt insgesamt 5 Level.

```mermaid
classDiagram
    MonoBehaviour <|-- Ball
    MonoBehaviour <|-- Block
    MonoBehaviour <|-- GameSession
    MonoBehaviour <|-- Level
    MonoBehaviour <|-- LoseCollider
    MonoBehaviour <|-- Paddle
    MonoBehaviour <|-- SceneLoader

    class Ball {
        + paddle1: Paddle
        + xPush: float
        + yPush: float
        + ballSounds: AudioClip
        + randomFactor: float
        - paddleToBallVector: Vector2
        - hasStarted: bool
        - myAudioSource: AudioSource
        - myRigidBody2D: RIgidbody2D 
        - Start() void 
        - Update() void 
        - LaunchOnMouseClick() void 
        - LockBallToPaddle() void 
        - OnCollisionEnter2D() void 
    }
    class Block {
        - BREAKABLE: const string
        - UNBREAKABLE: const string
        + breakSound: AudioClip
        + blockSparklesVFX: GameObject
        + hitSprites: Sprite
        - level: level
        - gameStatus: GameSession
        - timesHit: int
        - Start() void 
        - CountBreakableBlocks() void 
        - OnCollisionEnter2D() void 
        - HandleHit() void 
        - ShowNextHitSprite() void 
        - DestroyBlock() void 
        - PlayBlockDestroySFX() void 
        - TriggerSparkleVFX() void 
    }
 
    class GameSession {
        + gameSpeed: float
        + pointsPerBlockDestroyed: int
        + scoreText: TextMeshProUGUI
        + isAutoPlayEnabled: bool
        + currentScore: int
        - Awake() void 
        - Start() void 
        - Update() void 
        + AddToScore() void 
        + ResetGame() void 
        + IsAutoPlayEnabled() bool
    }

    class Level{
        - breakableBlocks: int
        - sceneLoader: SceneLoader
        - Start() void 
        + CountBlocks() void 
        + BlockDestroyed() void 
        - LoadEndScreen() void 
    }

    class LoseCollider{
        + loader: GameObject
        - sceneLoader: SceneLoader
        - Start() void 
        - OnTriggerEnter2D() void 
    }

    class Paddle{
        + minX: float
        + maxX: float
        + screenWidthInUnits: float
        - theGameSession: GameSession
        - theBall: Ball
        - Start() void
        - Update() void
        - GetXPosition() float
    }
    class SceneLoader{
        - GAMEOVERSCREEN: const string
        - GONGRATSSCREEN: const string
        - LVEL5: const string
        + LoadNextScene() void
        + LoadWelcome() void
        + LoadGameOver() void
        + LoadCongrats() void
        + IsLastPlayScene() bool
     }
```
