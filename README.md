# Sleeper

![Sleeper icon](Assets/icon.png)

Customize skipping the night with an animation or voting.

**Version 1.11.0 targets Paper for Minecraft 26.3 and requires Java 25.**
See the [Paper Java requirements](https://docs.papermc.io/paper/getting-started/).
The existing Folia scheduler support is retained.

This is a compatibility update from 1.10.9: night skipping, voting, commands,
permissions, integrations and configuration defaults keep their existing behavior.

### Installation and upgrading

1. Stop the Paper server. When upgrading, back up `plugins/Sleeper/`.
2. Place `Sleeper-1.11.0.jar` in the server's `plugins/` directory. Remove the old
   Sleeper JAR so that only one version is installed.
3. Keep your existing `plugins/Sleeper/config.yml` when upgrading from 1.10.9;
   no configuration migration is required. On a new installation the file is
   generated on the first start.
4. Start Paper 26.3 using Java 25 and check that Sleeper 1.11.0 is enabled in the
   console. You can also check the installed version with `/version Sleeper`.

GSit, EssentialsX and JustAFK are optional server plugins; install compatible
versions separately if you use their integrations.

### Features of Sleeper

Configurable night skipping options:

- Skip at a configurable percentage of online players.
- Animate the night skip with a configurable speed.
- Use a voting system to decide skipping the night.

All the messages can be customized and formatted with color codes or MiniMessage.

Plugin integrations:

- Sleep by lying down with GSit when `GSitPoseToSleep` is enabled.
- Ignore AFK players with EssentialsX or [JustAFK 1.2.0+](https://github.com/CaptainRatax/JustAFK)
  when `IgnoreAFKPlayers` is enabled.

### Configuration

Edit `plugins/Sleeper/config.yml` and run `/sleep reload` to apply changes.
The [default configuration](src/main/resources/config.yml) documents all available
settings and messages.

- `SkipPercentage` controls the sleeping threshold per world (default: `25`).
  Creative, spectator, manually ignored and, when configured, AFK players are
  excluded from the eligible player count.
- `UseAnimation` and `SkipSpeed` control the night skip animation. `DelaySleep`
  and `DelaySeconds` control the delay before a sleeping player is counted.
- `DayTime` sets the target time; `NightTime` sets when voting and GSit sleeping
  are allowed.
- `VoteSkip` enables voting (default: `false`). `SkipVotePercent`, `YesMultiplier`
  and `NoMultiplier` control the threshold based on weighted yes votes minus no
  votes. `StartWithoutSleep` allows a vote command to start a vote at night;
  `AutomaticStart` starts votes automatically at night. `LimitedVoteTime` and
  `MaxVoteTime` optionally limit their duration.
- `FormattingType` accepts `minecraft` for `&` color codes or `minimessage` for
  MiniMessage formatting. Sleep and vote messages, action bars and vote displays
  are configurable in the same file.

### Commands and permissions

**Everyone**

- `sleeper.sleep` — `/sleep`: show available subcommands.
- `sleeper.vote` — `/sleep yes`, `/sleep no`, `/sleep votes`: vote or view the
  current world's vote counts. Voting requires `VoteSkip: true`.

Both permissions are granted to everyone by default.

**Admin**

- `sleeper.ignore` — `/sleep ignore [player] [true|false]`: toggle whether you or
  an online player are ignored, or explicitly set that player's ignored state.
- `sleeper.reload` — `/sleep reload`: reload plugin configuration.
- `sleeper.data` — `/sleep debug`: toggle debug messages and display sleep data.

These permissions are granted to operators by default. All subcommands also
require access to `/sleep` through `sleeper.sleep`. Voting and debug commands are
player-only; the console can reload configuration or change an online player's
ignored state.

### Building from source

Install a **JDK 25** and Apache Maven, and ensure Maven uses that JDK (check
`mvn -version`). From the project directory, run:

```sh
mvn clean package
```

The ready-to-install plugin is **`target/Sleeper-1.11.0.jar`**. Maven includes the
required bundled libraries in this JAR. Use this file in `plugins/`, rather than
`target/original-Sleeper-1.11.0.jar`, which is the unbundled build intermediate.
Paper and the optional integration plugins are provided by the server and are
not bundled.

### Contributing

Contributions are welcome via suggestions or pull requests. When making PRs please keep them to one change/issue per PR.
The project is licensed under GPL v3 and so are any contributions.
