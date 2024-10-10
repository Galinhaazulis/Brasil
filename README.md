-- Criação da Hub
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local TextLabel = Instance.new("TextLabel")
local ToggleButton = Instance.new("TextButton")
local CloseButton = Instance.new("TextButton")
local TeleportButton = Instance.new("TextButton")
local SpeedToggle = Instance.new("TextButton")

ScreenGui.Parent = game.CoreGui

Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
Frame.Position = UDim2.new(0, 0, 0.5, -50)
Frame.Size = UDim2.new(0, 200, 0, 150)
Frame.Active = true
Frame.Draggable = true

TextLabel.Parent = Frame
TextLabel.Size = UDim2.new(1, 0, 0.2, 0)
TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TextLabel.Text = "Minha Hub"
TextLabel.TextColor3 = Color3.fromRGB(0, 0, 0)

ToggleButton.Parent = Frame
ToggleButton.Size = UDim2.new(1, 0, 0.2, 0)
ToggleButton.Position = UDim2.new(0, 0, 0.2, 0)
ToggleButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
ToggleButton.Text = "Minimizar"
ToggleButton.TextColor3 = Color3.fromRGB(0, 0, 0)

CloseButton.Parent = Frame
CloseButton.Size = UDim2.new(1, 0, 0.2, 0)
CloseButton.Position = UDim2.new(0, 0, 0.4, 0)
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
CloseButton.Text = "Fechar"
CloseButton.TextColor3 = Color3.fromRGB(0, 0, 0)

TeleportButton.Parent = Frame
TeleportButton.Size = UDim2.new(1, 0, 0.2, 0)
TeleportButton.Position = UDim2.new(0, 0, 0.6, 0)
TeleportButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TeleportButton.Text = "Teleporte"
TeleportButton.TextColor3 = Color3.fromRGB(0, 0, 0)

SpeedToggle.Parent = Frame
SpeedToggle.Size = UDim2.new(1, 0, 0.2, 0)
SpeedToggle.Position = UDim2.new(0, 0, 0.8, 0)
SpeedToggle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
SpeedToggle.Text = "Ativar Super Velocidade"
SpeedToggle.TextColor3 = Color3.fromRGB(0, 0, 0)

-- Função para minimizar/maximizar a hub
local minimized = false
ToggleButton.MouseButton1Click:Connect(function()
    minimized = not minimized
    if minimized then
        Frame.Size = UDim2.new(0, 200, 0, 25)
        ToggleButton.Text = "Maximizar"
    else
        Frame.Size = UDim2.new(0, 200, 0, 150)
        ToggleButton.Text = "Minimizar"
    end
end)

-- Função para fechar a hub
CloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

-- Função para teleporte
TeleportButton.MouseButton1Click:Connect(function()
    local player = game.Players.LocalPlayer
    local destination = Vector3.new(0, 0, 0) -- Substitua com as coordenadas do local desejado
    local speed = 34 -- Velocidade de 34 km/h
    local distance = (destination - player.Character.HumanoidRootPart.Position).magnitude
    local duration = distance / speed

    local tweenService = game:GetService("TweenService")
    local tweenInfo = TweenInfo.new(duration, Enum.EasingStyle.Linear)
    local goal = {CFrame = CFrame.new(destination)}

    local tween = tweenService:Create(player.Character.HumanoidRootPart, tweenInfo, goal)
    tween:Play()
end)

-- Função para ativar/desativar super velocidade
local speedEnabled = false
SpeedToggle.MouseButton1Click:Connect(function()
    speedEnabled = not speedEnabled
    local player = game.Players.LocalPlayer
    if speedEnabled then
        SpeedToggle.Text = "Desativar Super Velocidade"
        player.Character.Humanoid.WalkSpeed = 34
    else
        SpeedToggle.Text = "Ativar Super Velocidade"
        player.Character.Humanoid.WalkSpeed = 16 -- Velocidade padrão
    end
end)
