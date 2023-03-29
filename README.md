# Logger-Loader-OpenSource
一群傻逼写的低能死妈废物东西被你野爹三秒逆开的废物loader开源 还有 别以为你们有多高贵 操你妈先看看你的dll的源码哪里来的把 还有 傻逼玩意写你吗挂呢 还有那个a什么的还不认识你野爹是谁呢 操你妈的倒卖死亲妈 不遵守开源许可证你妈就死了 
## Java层
```Java
package com.netease.mc.modSS;

import org.objectweb.asm.*;
import net.minecraft.launchwrapper.*;
import java.security.*;
import java.lang.reflect.*;

public class RRRRRRX extends Thread
{
    private byte[][] classes;
    
    public RRRRRRX() {
        this.classes = null;
    }
    
    public RRRRRRX(final byte[][] classes) {
        this.classes = null;
        this.classes = classes;
        this.load();
    }
    
    public void load() {
        System.out.println("[NAC]Start Loading...");
        try {
            final Method RunTrans = LaunchClassLoader.class.getDeclaredMethod("runTransformers", String.class, String.class, byte[].class);
            RunTrans.setAccessible(true);
            for (final byte[] array : this.classes) {
                final ClassReader cr = new ClassReader(array);
                final String className = cr.getClassName().replaceAll("/", ".");
                final byte[] FORDEF = (byte[])RunTrans.invoke(Launch.classLoader, "net.minecraft.ezcheatfucknac", className, array);
                this.R(className, FORDEF, 0, FORDEF.length, Launch.classLoader.getClass().getProtectionDomain());
            }
            new ShellSock();
        }
        catch (Exception e) {
            e.printStackTrace();
        }
    }
    
    protected final Class<?> R(final String name, final byte[] b, final int off, final int len, ProtectionDomain protectionDomain) throws ClassFormatError, NoSuchMethodException, InvocationTargetException, IllegalAccessException {
        final Method preDefineClass = ClassLoader.class.getDeclaredMethod("preDefineClass", String.class, ProtectionDomain.class);
        final Method defineClassSourceLocation = ClassLoader.class.getDeclaredMethod("defineClassSourceLocation", ProtectionDomain.class);
        final Method defineClass1 = ClassLoader.class.getDeclaredMethod("defineClass1", String.class, byte[].class, Integer.TYPE, Integer.TYPE, ProtectionDomain.class, String.class);
        final Method postDefineClass = ClassLoader.class.getDeclaredMethod("postDefineClass", Class.class, ProtectionDomain.class);
        preDefineClass.setAccessible(true);
        defineClassSourceLocation.setAccessible(true);
        defineClass1.setAccessible(true);
        postDefineClass.setAccessible(true);
        protectionDomain = (ProtectionDomain)preDefineClass.invoke(Launch.classLoader, name, protectionDomain);
        final String source = (String)defineClassSourceLocation.invoke(Launch.classLoader, protectionDomain);
        final Class c = (Class)defineClass1.invoke(Launch.classLoader, name, b, off, len, protectionDomain, source);
        postDefineClass.invoke(Launch.classLoader, c, protectionDomain);
        return (Class<?>)c;
    }
}
```
## C++层
```cpp

int __fastcall sub_180001B80(JNIEnv_ *a1)
{
  HMODULE v2; // rdi
  char *JVM_GetClassNameUTF; // r13
  const struct JNINativeInterface_ *v4; // r8
  int v5; // esi
  int v6; // er14
  __int64 v7; // rdi
  __int64 v8; // rax
  const char *v9; // rax
  __int64 ClassClazz; // rax
  __int64 v11; // rdi
  __int64 v12; // rax
  __int64 ClassInstance; // r14
  __int64 v14; // rax
  __int64 v15; // rdi
  unsigned int v17; // edi
  __int64 v18; // rax
  __int64 v19; // rdi
  int v20; // er12
  int v21; // er15
  _DWORD *v22; // r14
  __int64 v23; // r13
  __int64 v24; // rdi
  char v25; // r15
  int v26; // edi
  __int64 i; // r14
  const char *loaderClass; // rax
  __int64 v29; // r14
  __int64 v30; // rdi
  __int64 v31; // [rsp+30h] [rbp-29h]
  _jvmtiEnv *jvmti; // [rsp+38h] [rbp-21h] BYREF
  __int64 v33; // [rsp+40h] [rbp-19h] BYREF
  __int64 v34; // [rsp+48h] [rbp-11h] BYREF
  char *Str; // [rsp+50h] [rbp-9h] BYREF
  JNIEnv_ *v36; // [rsp+58h] [rbp-1h] BYREF
  __int64 v37; // [rsp+60h] [rbp+7h] BYREF
  char v38[8]; // [rsp+68h] [rbp+Fh] BYREF
  char v39[8]; // [rsp+70h] [rbp+17h] BYREF
  int v40; // [rsp+78h] [rbp+1Fh] BYREF
  int v41; // [rsp+7Ch] [rbp+23h] BYREF

  v2 = GetModuleHandleA("jvm");
  JVM_GetClassNameUTF = (char *)GetProcAddress(v2, "JVM_GetClassNameUTF");
  Str = JVM_GetClassNameUTF;
  GetProcAddress(v2, "JVM_DefineClass");
  v4 = a1->functions;
  v5 = 0;
  jvmti = 0i64;
  v36 = 0i64;
  ((void (__fastcall *)(JNIEnv_ *, JNIEnv_ **))v4->GetJavaVM)(a1, &v36);
  ((void (__fastcall *)(JNIEnv_ *, _jvmtiEnv **, __int64))v36->functions->FindClass)(v36, &jvmti, 805372416i64);
  v34 = 0i64;
  ((void (__fastcall *)(_jvmtiEnv *, int *, __int64 *))jvmti->functions->GetLoadedClasses)(jvmti, &v40, &v33);
  v6 = 0;
  if ( v40 > 0 )
  {
    v7 = 0i64;
    do
    {
      ((void (__fastcall *)(_jvmtiEnv *, _QWORD, __int64 *))jvmti->functions->GetClassLoader)(
        jvmti,
        *(_QWORD *)(v7 + v33),
        &v34);
      if ( v34 )
      {
        v8 = ((__int64 (__fastcall *)(JNIEnv_ *))a1->functions->GetObjectClass)(a1);
        v9 = (const char *)((__int64 (__fastcall *)(JNIEnv_ *, __int64))JVM_GetClassNameUTF)(a1, v8);
        if ( strstr(v9, "LaunchClassLoader") )
          break;
      }
      ++v6;
      v7 += 8i64;
    }
    while ( v6 < v40 );
  }
  ((void (__fastcall *)(_jvmtiEnv *, __int64))jvmti->functions->Deallocate)(jvmti, v33);
  ClassClazz = ((__int64 (__fastcall *)(JNIEnv_ *, const char *))a1->functions->FindClass)(a1, "java/lang/Class");
  v11 = ((__int64 (__fastcall *)(JNIEnv_ *, __int64, const char *, const char *))a1->functions->GetMethodID)(
          a1,
          ClassClazz,
          "getProtectionDomain",
          "()Ljava/security/ProtectionDomain;");
  v12 = ((__int64 (__fastcall *)(JNIEnv_ *, const char *))a1->functions->FindClass)(a1, "java/lang/Class");
  ClassInstance = ((__int64 (__fastcall *)(JNIEnv_ *, __int64, const char *, const char *))a1->functions->GetMethodID)(
                    a1,
                    v12,
                    "newInstance",
                    "()Ljava/lang/Object;");
  if ( !ClassInstance )
    MessageBoxA(0i64, Text, "END", 1u);
  v14 = ((__int64 (__fastcall *)(JNIEnv_ *, __int64))a1->functions->GetObjectClass)(a1, v34);
  sub_180001B20(a1, v14, v11);
  v15 = ((__int64 (__fastcall *)(JNIEnv_ *, _QWORD, __int64, char *, int))a1->functions->DefineClass)(
          a1,
          0i64,
          v34,
          asc_1801927F0,
          dword_1801927E4);
  if ( !sub_180001B20(a1, v15, ClassInstance) )
    MessageBoxA(0i64, "classLoaderClazz iNSTANCE is NULL!", "fg", 1u);
  if ( !v15 )
    return MessageBoxA(0i64, "Loader is  not Defined!", "END", 1u);
  v17 = dword_1801927E0;
  v18 = ((__int64 (__fastcall *)(JNIEnv_ *, void *))a1->functions->FindClass)(a1, &unk_180008214);
  v19 = ((__int64 (__fastcall *)(JNIEnv_ *, _QWORD, __int64, _QWORD))a1->functions->NewObjectArray)(a1, v17, v18, 0i64);
  v20 = 0;
  v21 = 0;
  if ( ((unsigned __int8 (__fastcall *)(JNIEnv_ *))a1->functions->ExceptionCheck)(a1) )
    v19 = 0i64;
  v31 = v19;
  if ( dword_1801927E0 > 0 )
  {
    v22 = &unk_180192360;
    v23 = v19;
    do
    {
      v24 = ((__int64 (__fastcall *)(JNIEnv_ *, _QWORD))a1->functions->NewByteArray)(a1, (unsigned int)*v22);
      ((void (__fastcall *)(JNIEnv_ *, __int64, _QWORD, _QWORD, char *))a1->functions->SetByteArrayRegion)(
        a1,
        v24,
        0i64,
        (unsigned int)*v22,
        &asc_18004F000[v20]);
      v20 += *v22;
      ((void (__fastcall *)(JNIEnv_ *, __int64, _QWORD, __int64))a1->functions->SetObjectArrayElement)(
        a1,
        v23,
        (unsigned int)v21++,
        v24);
      ++v22;
    }
    while ( v21 < dword_1801927E0 );
    JVM_GetClassNameUTF = Str;
    v5 = 0;
  }
  v25 = 0;
  ((void (__fastcall *)(_jvmtiEnv *, int *, __int64 *))jvmti->functions->GetLoadedClasses)(jvmti, &v40, &v33);
  v26 = 0;
  if ( v40 > 0 )
  {
    for ( i = 0i64; ; i += 8i64 )
    {
      loaderClass = (const char *)((__int64 (__fastcall *)(JNIEnv_ *, _QWORD))JVM_GetClassNameUTF)(
                                    a1,
                                    *(_QWORD *)(i + v33));
      if ( strstr(loaderClass, "com/netease/mc/modSS/RRR") )
        break;
      if ( ++v26 >= v40 )
        return MessageBoxA(0i64, "get constructor failed", "fg", 1u);
    }
    v29 = 8i64 * v26;
    ((void (__fastcall *)(_jvmtiEnv *, _QWORD, int *, __int64 *))jvmti->functions->GetClassMethods)(
      jvmti,
      *(_QWORD *)(v29 + v33),
      &v41,
      &v37);
    if ( v41 > 0 )
    {
      v30 = 0i64;
      do
      {
        ((void (__fastcall *)(_jvmtiEnv *, _QWORD, char **, char *, char *))jvmti->functions->GetMethodName)(
          jvmti,
          *(_QWORD *)(v30 + v37),
          &Str,
          v39,
          v38);
        if ( strstr(Str, "init") )
        {
          if ( v25 )
            return sub_180001B50(a1, *(_QWORD *)(v29 + v33), *(_QWORD *)(v37 + 8i64 * v5), v31);
          v25 = 1;
        }
        ++v5;
        v30 += 8i64;
      }
      while ( v5 < v41 );
    }
  }
  return MessageBoxA(0i64, "get constructor failed", "fg", 1u);
}
```
