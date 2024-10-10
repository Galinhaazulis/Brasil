-- Criação da Hub
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local TextLabel = Instance.new("TextLabel")
local ToggleButton = Instance.new("TextButton")
local MoneyBagToggle = Instance.new("TextButton")

ScreenGui.Parent = game.CoreGui

Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
Frame.Position = UDim2.new(0, 0, 0.5, -50)
Frame.Size = UDim2.new(0, 200, 0, 100)
Frame.Active = true
Frame.Draggable = true

TextLabel.Parent = Frame
TextLabel.Size = UDim2.new(1, 0, 0.5, 0)
TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TextLabel.Text = "Minha Hub"
TextLabel.TextColor3 = Color3.fromRGB(0, 0, 0)

ToggleButton.Parent = Frame
ToggleButton.Size = UDim2.new(1, 0, 0.25, 0)
ToggleButton.Position = UDim2.new(0, 0, 0.5, 0)
ToggleButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
ToggleButton.Text = "Minimizar"
ToggleButton.TextColor3 = Color3.fromRGB(0, 0, 0)

MoneyBagToggle.Parent = Frame
MoneyBagToggle.Size = UDim2.new(1, 0, 0.25, 0)
MoneyBagToggle.Position = UDim2.new(0, 0, 0.75, 0)
MoneyBagToggle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
MoneyBagToggle.Text = "Ativar Bolsa 20k"
MoneyBagToggle.TextColor3 = Color3.fromRGB(0, 0, 0)

-- Função para minimizar/maximizar a hub
local minimized = false
ToggleButton.MouseButton1Click:Connect(function()
    minimized = not minimized
    if minimized then
        Frame.Size = UDim2.new(0, 200, 0, 25)
        ToggleButton.Text = "Maximizar"
    else
        Frame.Size = UDim2.new(0, 200, 0, 100)
        ToggleButton.Text = "Minimizar"
    end
end)

-- Função para ativar/desativar a bolsa de 20k
local moneyBagEnabled = false
MoneyBagToggle.MouseButton1Click:Connect(function()
    moneyBagEnabled = not moneyBagEnabled
    if moneyBagEnabled then
        MoneyBagToggle.Text = "Desativar Bolsa 20k"
        -- Código para aumentar a capacidade da bolsa para 20k
        game.Players.LocalPlayer.Backpack.MoneyBag.Capacity.Value = 20000
    else
        MoneyBagToggle.Text = "Ativar Bolsa 20k"
        -- Código para restaurar a capacidade original da bolsa
        game.Players.LocalPlayer.Backpack.MoneyBag.Capacity.Value = 100
    end
end)
