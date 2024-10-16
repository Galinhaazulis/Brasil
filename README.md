-- Script de teleporte em Lua para "E.B Exército Brasileiro" no Roblox

-- Função para criar um ponto de teleporte
function criarTeleporte(nome, x, y, z)
    return {
        nome = nome,
        posicao = {x = x, y = y, z = z}
    }
end

-- Função para teletransportar um jogador para um ponto específico
function teletransportar(jogador, teleporte)
    jogador.Character:SetPrimaryPartCFrame(CFrame.new(teleporte.posicao.x, teleporte.posicao.y, teleporte.posicao.z))
    print(jogador.Name .. " foi teletransportado para " .. teleporte.nome)
end

-- Definindo os pontos de teleporte com coordenadas específicas do jogo
entradaCofre = criarTeleporte("Entrada do Cofre", 120, 30, 45)
entregaDinheiro = criarTeleporte("Entrega de Dinheiro", 200, 40, 75)

-- Criando a interface da hub
local ScreenGui = Instance.new("ScreenGui")
local TeleportFrame = Instance.new("Frame")
local TeleportButton1 = Instance.new("TextButton")
local TeleportButton2 = Instance.new("TextButton")

-- Configurando a interface
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

TeleportFrame.Size = UDim2.new(0, 200, 0, 100)
TeleportFrame.Position = UDim2.new(0.5, -100, 0.5, -50)
TeleportFrame.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
TeleportFrame.Active = true
TeleportFrame.Draggable = true
TeleportFrame.Parent = ScreenGui

TeleportButton1.Size = UDim2.new(0, 180, 0, 40)
TeleportButton1.Position = UDim2.new(0, 10, 0, 10)
TeleportButton1.Text = "Ir para Entrada do Cofre"
TeleportButton1.Parent = TeleportFrame

TeleportButton2.Size = UDim2.new(0, 180, 0, 40)
TeleportButton2.Position = UDim2.new(0, 10, 0, 50)
TeleportButton2.Text = "Ir para Entrega de Dinheiro"
TeleportButton2.Parent = TeleportFrame

-- Funções dos botões
TeleportButton1.MouseButton1Click:Connect(function()
    teletransportar(game.Players.LocalPlayer, entradaCofre)
end)

TeleportButton2.MouseButton1Click:Connect(function()
    teletransportar(game.Players.LocalPlayer, entregaDinheiro)
end)
