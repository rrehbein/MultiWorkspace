# MultiWorkspace

Individual mods should be 'git cloned' inside subfolders of this project.
Modify settings.gradle for all your mods.
Inside the mods/build.gradle you should have the following construct to make sure the mods are still compilable standalone as well as inside the multi-project:

    if (findProject(':McJtyLib') != null) {
        implementation project(':McJtyLib')
    } else {
        implementation fg.deobf (project.dependencies.create("com.github.mcjty:mcjtylib:${mcjtylib_version}") {
            transitive = false
        })
    }

To setup this project, just open the root (empty) build.gradle as a project in IDEA. Run genIntellijRuns and select the one for the 'workspace' module

For testing subproject version updates, include `-P` arguments your build. For example:

    ./gradlew build -Pforge_version=39.0.8
    ./gradlew runClient -Pforge_version=39.0.8
