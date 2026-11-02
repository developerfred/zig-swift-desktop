# Zig Swift Desktop

Framework multi-agente desktop nativo para macOS — algo como Electron, mas para **Zig + SwiftUI**.

Cuida automaticamente de:
- Ponte Zig ↔ Swift (C ABI)
- Comunicação entre processos (IPC)
- Múltiplas janelas
- Ciclo de vida de agentes
- Empacotamento como `.app` bundle

## Arquitetura

```
zig-swift-desktop/
├── README.md
├── LICENSE
├── Package.swift
├── Sources/
│   ├── ZigDesktopCore/        # Núcleo em Zig (agentes, mensagens, estado)
│   │   ├── agent.zig
│   │   ├── ipc.zig
│   │   └── bridge.zig
│   ├── SwiftDesktopKit/       # Framework SwiftUI para UI
│   │   ├── DesktopView.swift
│   │   ├── AgentWindow.swift
│   │   └── IPCBridge.swift
│   └── main.swift             # Entry point
├── Tests/
└── example/
    └── multi-agent-app/
```

## Funcionalidades

- ✅ Múltiplos agentes rodando simultaneamente
- ✅ Cada agente em sua própria janela SwiftUI
- ✅ IPC nativo entre agentes (mensagens assíncronas)
- ✅ Compartilhamento de estado entre agentes
- ✅ Empacotamento automático como `.app` macOS
- ✅ Suporte a UTF-8 completo (CJK, emoji, árabe)

## Uso rápido

```swift
import SwiftDesktopKit

// Cria um agente desktop
let agent = try DesktopAgent.create(
    id: "agent-1",
    name: "Vanderley Agent"
)

// Abre janela SwiftUI para este agente
agent.openWindow {
    ChatView(agent: agent)
}

// Envia mensagem para outro agente
try agent.sendMessage(to: "agent-2", text: "Hello from agent 1!")
```

```zig
// No núcleo Zig
export fn vanderley_agent_send(to: [*]const u8, msg: [*]const u8, len: c_int) c_int {
    // IPC entre agentes
}
```

## Requisitos

- macOS 15+
- Swift 6+
- Zig 0.17.0+

## Licença

MIT
