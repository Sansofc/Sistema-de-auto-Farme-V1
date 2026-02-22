# Sistema-de-auto-Farme-V1.0
-- Script de Teleporte Sequencial Automático - 84 Posições
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")
local rootPart = character:WaitForChild("HumanoidRootPart")

-- Lista completa das 84 posições
local positions = {
    -- P1 a P10
    Vector3.new(125.6, 12.5, 114.4),   -- P1
    Vector3.new(125.1, 27.0, 72.9),    -- P2
    Vector3.new(165.1, 21.5, 115.6),   -- P3
    Vector3.new(187.0, 33.0, 112.6),   -- P4
    Vector3.new(185.2, 39.0, 89.3),    -- P5
    Vector3.new(183.3, 42.0, 63.6),    -- P6
    Vector3.new(156.8, 42.0, 64.3),    -- P7
    Vector3.new(124.5, 64.0, 63.9),    -- P8
    Vector3.new(124.8, 64.1, 76.5),    -- P9
    Vector3.new(126.0, 73.0, 92.8),    -- P10
    
    -- P11 a P20
    Vector3.new(127.6, 73.0, 125.7),   -- P11
    Vector3.new(148.7, 75.1, 124.7),   -- P12
    Vector3.new(160.5, 77.5, 126.2),   -- P13
    Vector3.new(171.9, 84.5, 126.0),   -- P14
    Vector3.new(184.3, 89.5, 126.1),   -- P15
    Vector3.new(184.2, 93.0, 97.3),    -- P16
    Vector3.new(149.6, 93.0, 64.9),    -- P17
    Vector3.new(128.6, 109.0, 98.7),   -- P18
    Vector3.new(128.6, 109.0, 121.4),  -- P19
    Vector3.new(185.6, 123.0, 124.3),  -- P20
    
    -- P21 a P30
    Vector3.new(184.7, 126.0, 88.8),   -- P21
    Vector3.new(128.4, 127.0, 73.4),   -- P22
    Vector3.new(126.9, 140.9, 106.9),  -- P23
    Vector3.new(126.8, 144.9, 122.1),  -- P24
    Vector3.new(178.3, 144.9, 123.8),  -- P25
    Vector3.new(187.2, 151.0, 104.0),  -- P26
    Vector3.new(184.2, 165.5, 69.9),   -- P27
    Vector3.new(125.2, 165.5, 68.6),   -- P28
    Vector3.new(127.1, 183.0, 125.5),  -- P29
    Vector3.new(184.8, 183.0, 125.4),  -- P30
    
    -- P31 a P40
    Vector3.new(185.1, 184.0, 95.7),   -- P31
    Vector3.new(185.0, 184.0, 64.4),   -- P32
    Vector3.new(185.7, 184.0, 45.2),   -- P33
    Vector3.new(122.9, 184.0, 44.7),   -- P34
    Vector3.new(112.7, 184.0, 123.7),  -- P35
    Vector3.new(122.6, 205.0, 124.5),  -- P36
    Vector3.new(145.8, 214.0, 124.3),  -- P37
    Vector3.new(146.5, 223.0, 124.8),  -- P38
    Vector3.new(160.7, 224.9, 124.6),  -- P39
    Vector3.new(172.6, 224.9, 123.8),  -- P40
    
    -- P41 a P50
    Vector3.new(184.5, 224.6, 123.0),  -- P41
    Vector3.new(186.6, 285.0, 66.4),   -- P49
    Vector3.new(125.5, 303.0, 63.7),   -- P50
    Vector3.new(126.0, 314.0, 76.4),   -- P51
    Vector3.new(125.2, 314.0, 124.5),  -- P52
    Vector3.new(148.6, 314.0, 124.6),  -- P53
    Vector3.new(160.2, 324.5, 123.7),  -- P54
    Vector3.new(172.3, 324.5, 124.0),  -- P55
    Vector3.new(182.5, 324.5, 123.7),  -- P56
    Vector3.new(183.1, 333.0, 110.4),  -- P57
    
    -- P51 a P60 (renomeado para continuidade)
    Vector3.new(179.5, 339.0, 65.6),   -- P58
    Vector3.new(131.4, 354.0, 64.0),   -- P59
    Vector3.new(125.7, 364.0, 110.5),  -- P60
    Vector3.new(205.7, 364.0, 121.9),  -- P61
    Vector3.new(205.8, 364.0, 58.4),   -- P62
    Vector3.new(114.0, 364.0, 51.3),   -- P63
    Vector3.new(131.0, 379.0, 64.9),   -- P64
    Vector3.new(133.5, 384.0, 86.1),   -- P65
    Vector3.new(189.5, 386.0, 99.5),   -- P66
    Vector3.new(186.2, 401.0, 63.8),   -- P67
    
    -- P61 a P70
    Vector3.new(130.0, 408.0, 63.6),   -- P68
    Vector3.new(126.0, 426.0, 122.7),  -- P69
    Vector3.new(181.5, 426.0, 123.0),  -- P70
    Vector3.new(182.4, 445.0, 91.8),   -- P71
    Vector3.new(129.5, 445.0, 91.7),   -- P72
    Vector3.new(125.6, 460.0, 70.4),   -- P73
    Vector3.new(162.6, 460.0, 71.7),   -- P74
    Vector3.new(155.7, 481.0, 126.6),  -- P75
    Vector3.new(155.7, 483.0, 154.7),  -- P76
    Vector3.new(154.8, 483.0, 182.0),  -- P77
    
    -- P71 a P80
    Vector3.new(155.3, 483.0, 233.0),  -- P78
    Vector3.new(154.8, 480.3, 307.9),  -- P79
    Vector3.new(153.4, 77.0, 87.6),    -- P80
    Vector3.new(166.8, 81.0, 94.7),    -- P81
    Vector3.new(170.9, 168.5, 108.5),  -- P82
    Vector3.new(164.9, 163.5, 97.7),   -- P83
    Vector3.new(160.3, 163.5, 81.1)    -- P84
}

-- Configurações
local TELEPORT_DELAY = 0.03 -- 30 milissegundos
local sequenceRunning = false

-- Função para garantir que o personagem está completamente carregado
local function waitForCharacter()
    if not character or not character.Parent then
        character = player.CharacterAdded:Wait()
    end
    
    -- Aguarda todas as partes necessárias
    local parts = {"HumanoidRootPart", "Humanoid", "Head"}
    for _, partName in ipairs(parts) do
        local part = character:FindFirstChild(partName)
        if not part then
            character.ChildAdded:Wait(function(child)
                return child.Name == partName
            end)
        end
    end
    
    rootPart = character:WaitForChild("HumanoidRootPart")
    humanoid = character:WaitForChild("Humanoid")
    
    -- Aguarda o personagem estabilizar
    task.wait(0.1)
end

-- Função principal de teleporte sequencial
local function startTeleportSequence()
    if sequenceRunning then
        warn("Sequência já está em execução!")
        return
    end
    
    sequenceRunning = true
    
    -- Garante que o personagem está carregado
    waitForCharacter()
    
    -- Salva a posição original
    local originalPosition = rootPart.Position
    print("Posição original salva:", originalPosition)
    
    -- Verifica se há posições definidas
    if #positions == 0 then
        warn("Nenhuma posição definida na lista!")
        sequenceRunning = false
        return
    end
    
    print(string.format("Iniciando teleporte sequencial com %d posições...", #positions))
    print("Delay entre teleportes: " .. TELEPORT_DELAY * 1000 .. "ms")
    
    -- Teleporta para cada posição na sequência
    for i, targetPos in ipairs(positions) do
        -- Verifica se o personagem ainda existe
        if not character or not character.Parent then
            print("Personagem perdido durante execução. Reiniciando...")
            waitForCharacter()
        end
        
        -- Teleporta para a posição atual
        rootPart.CFrame = CFrame.new(targetPos)
        
        -- Mostra progresso a cada 10 posições
        if i % 10 == 0 or i == 1 or i == #positions then
            print(string.format("Progresso: %d/%d posições", i, #positions))
        end
        
        -- Pequena pausa entre teleportes
        task.wait(TELEPORT_DELAY)
    end
    
    -- Pequena pausa antes de retornar
    task.wait(TELEPORT_DELAY)
    
    -- Retorna à posição original
    rootPart.CFrame = CFrame.new(originalPosition)
    print("Retornado à posição original:", originalPosition)
    
    sequenceRunning = false
    print("✅ Sequência de teleporte concluída com sucesso!")
    print(string.format("Total de %d teleportes realizados", #positions))
end

-- Função para verificar a posição atual
local function getCurrentPosition()
    if rootPart then
        return rootPart.Position
    end
    return nil
end

-- Função para teleportar para uma posição específica da lista
local function teleportToPosition(index)
    if index >= 1 and index <= #positions then
        waitForCharacter()
        rootPart.CFrame = CFrame.new(positions[index])
        print(string.format("Teleportado para P%d: %s", index, tostring(positions[index])))
    else
        warn("Índice inválido! Use entre 1 e " .. #positions)
    end
end

-- Interface de execução
print("\n" .. string.rep("=", 50))
print("🚀 SCRIPT DE TELEPORTE SEQUENCIAL - 84 POSIÇÕES")
print(string.rep("=", 50))
print("📊 Posições configuradas: " .. #positions .. "/84")
print("⏱️  Delay entre teleportes: " .. TELEPORT_DELAY * 1000 .. "ms")
print("📌 Posição atual: " .. tostring(getCurrentPosition() or "N/A"))
print(string.rep("=", 50) .. "\n")

-- Inicia a sequência automaticamente
print("▶️ Iniciando sequência em 2 segundos...")
task.wait(2)
startTeleportSequence()

-- Comandos úteis (descomente para usar):
-- startTeleportSequence()  -- Inicia a sequência
-- teleportToPosition(1)    -- Teleporta para P1
-- teleportToPosition(42)   -- Teleporta para P42
-- print("Posição atual:", getCurrentPosition())  -- Mostra posição atual
