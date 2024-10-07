-- Cria a GUI
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local CloseButton = Instance.new("TextButton")
local SpeedButton = Instance.new("TextButton")
local FlyButton = Instance.new("TextButton")
local Dropdown = Instance.new("TextButton")
local AllyButton = Instance.new("TextButton")
local AllyDropdown = Instance.new("TextButton")
local AimbotButton = Instance.new("TextButton")
local FarmDropdown = Instance.new("TextButton")
local AntiLagDropdown = Instance.new("TextButton")
local NoClipButton = Instance.new("TextButton")
local AutoHealButton = Instance.new("TextButton")
local AntiVoidButton = Instance.new("TextButton")
local RejoinButton = Instance.new("TextButton")
local ESPButton = Instance.new("TextButton")

-- Configura a GUI
ScreenGui.Parent = game.CoreGui
Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
Frame.Position = UDim2.new(0.5, -100, 0.5, -375)
Frame.Size = UDim2.new(0, 200, 0, 750)
Frame.Active = true
Frame.Draggable = true

CloseButton.Parent = Frame
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
CloseButton.Position = UDim2.new(1, -25, 0, 0)
CloseButton.Size = UDim2.new(0, 25, 0, 25)
CloseButton.Text = "X"

local buttons = {
    {SpeedButton, "Aumentar Velocidade"},
    {FlyButton, "Voar"},
    {Dropdown, "Selecionar Local"},
    {AllyButton, "Selecionar Aliado"},
    {AllyDropdown, "Aliado"},
    {AimbotButton, "Ativar Aimbot"},
    {FarmDropdown, "Selecionar Farm"},
    {AntiLagDropdown, "Anti-Lag"},
    {NoClipButton, "No-Clip"},
    {AutoHealButton, "Auto-Heal"},
    {AntiVoidButton, "Anti-Void"},
    {RejoinButton, "Rejoin"},
    {ESPButton, "ESP"}
}

for i, buttonData in ipairs(buttons) do
    local button = buttonData[1]
    local text = buttonData[2]
    button.Parent = Frame
    button.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
    button.Position = UDim2.new(0.5, -50, 0, 35 + (i - 1) * 60)
    button.Size = UDim2.new(0, 100, 0, 50)
    button.Text = text
end

-- Função para aumentar a velocidade
local function aumentarVelocidade()
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    local humanoid = character:WaitForChild("Humanoid")
    humanoid.WalkSpeed = 50 -- Define a velocidade de caminhada para 50
end

SpeedButton.MouseButton1Click:Connect(aumentarVelocidade)

-- Função para voar
local function voar()
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
    local flySpeed = 30 / 3.6 -- Converte 30 km/h para m/s

    local flying = true
    local bodyVelocity = Instance.new("BodyVelocity")
    bodyVelocity.Velocity = Vector3.new(0, flySpeed, 0)
    bodyVelocity.MaxForce = Vector3.new(4000, 4000, 4000)
    bodyVelocity.Parent = humanoidRootPart

    game:GetService("RunService").Stepped:Connect(function()
        if flying then
            humanoidRootPart.CFrame = humanoidRootPart.CFrame + humanoidRootPart.CFrame.LookVector * flySpeed * game:GetService("RunService").Stepped:Wait()
        else
            bodyVelocity:Destroy()
        end
    end)

    FlyButton.MouseButton1Click:Connect(function()
        flying = not flying
        if not flying then
            bodyVelocity:Destroy()
        end
    end)
end

FlyButton.MouseButton1Click:Connect(voar)

-- Função para fechar a GUI
CloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)
