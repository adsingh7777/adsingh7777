# Java Program to play Sa RE GA MA PA DA NI SA from laptop keyboard.
```import javax.sound.midi.*;

public class Piano {
    public static void main(String[] args) {
         try {
                // Get the default Synthesizer
                Synthesizer synthesizer = MidiSystem.getSynthesizer();
                synthesizer.open();

                // Get the default Instrument
                Instrument[] instruments =   synthesizer.getLoadedInstruments();
                MidiChannel channel = synthesizer.getChannels()[0];
                channel.programChange(instruments[0].getPatch().getProgram());

                // Map keys to MIDI note numbers
                int[] noteMap = { 60, 62, 64, 65, 67, 69, 71, 72 }; // C, D, E, F, G, A, B, C (next octave)

                // Listen for key presses
                while (true) {
                    int keyCode = System.in.read();
                    System.out.println("listening");
                    if (keyCode == 's') {
                        channel.noteOn(noteMap[0], 100); //Play note C (Sa)
                    } else if (keyCode == 'r') {
                        channel.noteOn(noteMap[1], 100); // Play note D (Re)
                    } else if (keyCode == 'g') {
                        channel.noteOn(noteMap[2], 100); // Play note E (Ga)
                    } else if (keyCode == 'm') {
                        channel.noteOn(noteMap[3], 100); // Play note F (Ma)
                    } else if (keyCode == 'p') {
                        channel.noteOn(noteMap[4], 100); // Play note G (Pa)
                    } else if (keyCode == 'd') {
                        channel.noteOn(noteMap[5], 100); // Play note A (Dha)
                    } else if (keyCode == 'n') {
                        channel.noteOn(noteMap[6], 100); // Play note B (Ni)
                    } else if (keyCode == 's' + 128) {
                        channel.noteOn(noteMap[7], 100); // Play note C (Sa) of next octave
                    } else {
                        // Release the note after a short delay
                        try {
                            Thread.sleep(200);
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                        channel.noteOff(noteMap[0]);
                        channel.noteOff(noteMap[1]);
                        channel.noteOff(noteMap[2]);
                        channel.noteOff(noteMap[3]);
                        channel.noteOff(noteMap[4]);
                        channel.noteOff(noteMap[5]);
                        channel.noteOff(noteMap[6]);
                        channel.noteOff(noteMap[7]);
                    }
                }
            } catch (Exception e) {
                e.printStackTrace();
            }
    }

}
```

### Steps for buiding and runining the code is as followed.
1. save the code in file using class name as a file name Piano.java
2. Build the code using below command.
   ```
   javac Piano.java
   ```
3. After Building the code we will have the Piano.class file
4. Now create menifest.txt file for telling the jar about main class execution
```
vim manifest.txt
Main-Class: Piano
```
5. Now create jar file using the below command
   ```
   jar cvfm Piano.jar manifest.txt Piano.class
    ```
In the command jar cvfm Piano.jar manifest.txt Piano.class </br>

**c**: This option creates a new JAR file named Piano.jar. </br>
**v**: This option generates verbose output, which means it displays detailed information about the files being included in the JAR file. </br>
**f**: This option specifies the JAR file's name, Piano.jar. </br>
**m**: This option specifies that the next argument (manifest.txt) is the name of the manifest file to be used. </br>
**manifest.txt**: This is the name of the manifest file containing information about the JAR file. It typically includes metadata such as the Main-Class attribute, which specifies the main class to be executed when the JAR file is launched. </br>
**Piano.class**: This specifies the class file to be included in the JAR file. </br>

6. After creating the JAR file, you can verify its contents:
   ```
   jar tf Piano.jar
   ```
   This command lists the contents of the JAR file to ensure that the Piano.class file (and other class files, if any) are present.

7. Now run the JAR file using the java -jar command
   ```
   java -jar Piano.jar
   ```

### Test Cases

| SNo. | Test Case  | Input Keys                                  | Expected Output                                      | Result | Remarks |
|------|------------|---------------------------------------------|------------------------------------------------------|--------|---------|
| 1    | Test Case 1| Press keys `s r g m p d n s`               | Should hear notes "Sa Re Ga Ma Pa Dha Ni Sa" in sequence | Pass   |         |
| 2    | Test Case 2| Press keys `s r g m` (incomplete sequence) | Should hear notes "Sa Re Ga Ma" in sequence          | Pass   |         |
| 3    | Test Case 3| Press keys `s r g m p d n s s` (with repeat of Sa) | Should hear notes "Sa Re Ga Ma Pa Dha Ni Sa" in sequence | Pass   |         |
| 4    | Test Case 4| Press keys `s s s s s s s s` (continuous Sa) | Should continuously play note "Sa"                 | Pass   |         |
| 5    | Test Case 5| Press keys `s s s s` (short sequence)    | Should hear notes "Sa Sa Sa Sa" in sequence         | Pass   |         |
| 6    | Test Case 6| Press keys `s s s s r r r r` (Sa and Re sequence) | Should hear notes "Sa Sa Sa Sa Re Re Re Re" in sequence | Pass   |         |
