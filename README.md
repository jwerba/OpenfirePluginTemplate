# OpenfirePluginTemplate

In order to make plugin development independent from being inside the Openfire source code and give the oportunity to have plugins in a separated project you can apply the attached path to Openfire code (just a few harmless lines of code) you give PluginManager the ability to search the entire ClassPath of the project for Plugin.xml files (new [private void findPluginXmlFiles()] method) and in line with the current logic uses the already existing [private void loadPlugin(File pluginDir)] method to load any plugin in the classpath with no need to package the jars and put then inside the Plugins directory (usually /target/openfire/plugins).

Now you can have in your IDE workspace the Openfire project and another project for your plugin/s and the only thing yoy have to do to run it (and debug it) inside Openfire is add this plugin project/s to the classpath of the Openfire project.

If you do this you can clone this template and develop your Openfire Plugin in a more organized way.

1) Apply this patch to your Openfire source code and start using this template to develop your Plugin.

    https://github.com/jwerba/OpenfirePluginTemplate/blob/master/load%20plugins%20in%20classapath.patch
2) Edit your Openfire project and add this new project to the classpath

3) Code, debug, run Openfire and watch how your plugin is loaded. Place a breakpoint in your Plugin code and watch how you can debug it when you run your Openfire code.
    
4) Package the Plugin for deployment

    Create a maven run configuration with the following goals:
    package assembly:single

    The result will be a .jar with the structure that Openfire expects for a Plugin
    - plugin.xml
    - any other files inside src\main\resources
    - lib\
        - jar dependencies
        - plugin jar


5) Copy this artifact (the result of the previous item) inside your Openfire \plugins folder as any other plugin and watch how it is unzipped and detected by Openfire!
