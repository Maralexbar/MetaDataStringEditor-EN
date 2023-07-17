# global-metadata.dat String Modification Tool

- Fork of [MetaDataStringEditor](https://github.com/Perfare/Il2CppDumper) Using machine translation, there may be errors<br>

This is a simple tool for modifying the strings in the global-metadata.dat file, which contains the strings of text present in Android games exported with the Unity-il2cpp script backend.

## References

- [il2cppdumper](https://github.com/Perfare/Il2CppDumper)<br>
Understanding of the content of this file is based on the source code of this tool. Il2CppDumper is used to extract class definitions from compiled libil2cpp.so and global-metadata.dat files, generating renaming scripts compatible with IDA, DLLs usable with UABE and AssetStudio, among others. It is a very useful tool.

## Modification Content

In the global-metadata.dat file, the strings present in the code are stored as follows: there is a header list that holds the offset and length information of each string, and then there is a data section that directly compactly stores all the strings. Since there is a header list, there is no need for null termination (\0) at the end of the strings.

Since the number of strings does not change after modification, a direct modification is done on the list by overwriting the values in the original region. The length of the data section may change; if, after modification, the length is smaller or equal to the original length, it is directly overwritten in place. If the length is larger, it is written at the end of the file.
