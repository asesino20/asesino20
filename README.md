#NoEnv
SetWorkingDir %A_ScriptDir%
CoordMode, Pixel, Window
SetTitleMatchMode, 2
#SingleInstance Force
SetBatchLines, -1
#Persistent

; Ajusta estas coordenadas según tu configuración de PS Remote Play
global X := 960
global Y := 540

WinWaitActive, PS Remote Play

; Función para simular la pulsación de un botón
PressButton(key, duration := 50) {
    Send, {%key% down}
    Sleep, %duration%
    Send, {%key% up}
    Sleep, 50
}

; Función para esperar antes de que comience la canción
WaitForSong() {
    Sleep, 5000  ; Espera 5 segundos antes de que comience la canción
}

; Script para Dearly Beloved
DearlyBeloved() {
    WaitForSong()

    ; Introducción lenta
    Loop, 4 {
        PressButton("Z", 100)
        Sleep, 1900  ; Espera larga entre notas al principio
    }

    ; Sección principal
    Loop, 32 {
        PressButton("Z", 100)
        Sleep, 900  ; Ritmo más constante

        if (A_Index % 4 == 0) {  ; Cada 4 notas
            PressButton("X", 100)  ; Acción especial ocasional
            Sleep, 100
        }
    }

    ; Sección de puente
    Loop, 16 {
        PressButton("Z", 100)
        Sleep, 700  ; Ritmo ligeramente más rápido

        if (A_Index % 8 == 0) {  ; Cada 8 notas
            PressButton("C", 100)  ; Otra acción especial
            Sleep, 100
        }
    }

    ; Sección final
    Loop, 8 {
        PressButton("Z", 100)
        Sleep, 1100  ; Vuelve a un ritmo más lento para el final
    }
}

; Hotkey para iniciar Dearly Beloved
^1::
DearlyBeloved()
return

; Hotkey para detener el script
F2::
Reload
return

; Hotkey para salir del script completamente
F3::ExitApp

<!---
asesino20/asesino20 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
