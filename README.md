-- Cria uma nova ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "CloseGui"
screenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

-- Cria um Frame para conter o botão
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 200, 0, 100)
frame.Position = UDim2.new(0.5, -100, 0.5, -50)
frame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
frame.Parent = screenGui

-- Cria um botão para fechar a GUI
local closeButton = Instance.new("TextButton")
closeButton.Size = UDim2.new(0, 100, 0, 50)
closeButton.Position = UDim2.new(0.5, -50, 0.5, -25)
closeButton.Text = "Fechar"
closeButton.Parent = frame

-- Função para fechar a GUI quando o botão for clicado
closeButton.MouseButton1Click:Connect(function()
    screenGui:Destroy()
end)
