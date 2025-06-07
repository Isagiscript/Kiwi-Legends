local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")

-- Criar GUI principal
local gui2 = Instance.new("ScreenGui")
gui2.Name = "NinjaLegendsKIWI"
gui2.Parent = PlayerGui

local gui2Frame = Instance.new("Frame")
gui2Frame.Size = UDim2.new(0, 220, 0, 320) -- aumentei altura para os botões extras
gui2Frame.Position = UDim2.new(0.05, 0, 0.05, 0)
gui2Frame.BackgroundColor3 = Color3.fromRGB(40, 42, 54)
gui2Frame.BorderSizePixel = 0
gui2Frame.Active = true
gui2Frame.Draggable = true
gui2Frame.Parent = gui2

-- Sombra suave
local shadow = Instance.new("ImageLabel")
shadow.Size = UDim2.new(1, 20, 1, 20)
shadow.Position = UDim2.new(0, -10, 0, -10)
shadow.BackgroundTransparency = 1
shadow.Image = "rbxassetid://1316045217"
shadow.ImageColor3 = Color3.fromRGB(0, 0, 0)
shadow.ImageTransparency = 0.7
shadow.ScaleType = Enum.ScaleType.Slice
shadow.SliceCenter = Rect.new(10, 10, 118, 118)
shadow.Parent = gui2Frame

-- Título
local gui2Title = Instance.new("TextLabel")
gui2Title.Size = UDim2.new(1, 0, 0, 25)
gui2Title.BackgroundColor3 = Color3.fromRGB(60, 63, 80)
gui2Title.BorderSizePixel = 0
gui2Title.Text = "Ninja Legends KIWI"
gui2Title.TextColor3 = Color3.fromRGB(255, 255, 255)
gui2Title.Font = Enum.Font.GothamBold
gui2Title.TextSize = 16
gui2Title.Parent = gui2Frame

-- Função para criar botões
local function createButton(text, positionY)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1, -20, 0, 30)
    btn.Position = UDim2.new(0, 10, 0, positionY)
    btn.BackgroundColor3 = Color3.fromRGB(98, 102, 129)
    btn.BorderSizePixel = 0
    btn.Text = text
    btn.TextColor3 = Color3.fromRGB(240, 240, 240)
    btn.Font = Enum.Font.Gotham
    btn.TextSize = 14
    btn.AutoButtonColor = true
    btn.Parent = gui2Frame
    return btn
end

-- Botões principais
local toggleButton = createButton("Toggle Master Elements", 40)
local startButton = createButton("Start", 80)

local numberEntry = Instance.new("TextBox")
numberEntry.Size = UDim2.new(1, -20, 0, 30)
numberEntry.Position = UDim2.new(0, 10, 0, 120)
numberEntry.BackgroundColor3 = Color3.fromRGB(70, 73, 94)
numberEntry.BorderSizePixel = 0
numberEntry.PlaceholderText = "Enter number"
numberEntry.TextColor3 = Color3.fromRGB(230, 230, 230)
numberEntry.Font = Enum.Font.Gotham
numberEntry.TextSize = 14
numberEntry.ClearTextOnFocus = true
numberEntry.Parent = gui2Frame

local submitButton = createButton("Submit", 160)
local discordButton = createButton("KIWI MENU x LUAN", 200)
discordButton.BackgroundColor3 = Color3.fromRGB(72, 102, 163)

-- Botões extras
local jumpButton = createButton("Pulo Infinito", 240)
local speedButton = createButton("Correr Rápido", 280)

-- Botões de janela
local closeButton = Instance.new("TextButton")
closeButton.Size = UDim2.new(0, 30, 0, 25)
closeButton.Position = UDim2.new(1, -35, 0, 5)
closeButton.BackgroundColor3 = Color3.fromRGB(255, 75, 75)
closeButton.Text = "X"
closeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
closeButton.Font = Enum.Font.GothamBold
closeButton.TextSize = 18
closeButton.BorderSizePixel = 0
closeButton.Parent = gui2Frame

local minimizeButton = Instance.new("TextButton")
minimizeButton.Size = UDim2.new(0, 30, 0, 25)
minimizeButton.Position = UDim2.new(1, -70, 0, 5)
minimizeButton.BackgroundColor3 = Color3.fromRGB(200, 200, 70)
minimizeButton.Text = "-"
minimizeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
minimizeButton.Font = Enum.Font.GothamBold
minimizeButton.TextSize = 22
minimizeButton.BorderSizePixel = 0
minimizeButton.Parent = gui2Frame

-- Função do botão Start: envia o valor máximo positivo double
startButton.MouseButton1Click:Connect(function()
    local args = {
        [1] = "convertGems",
        [2] = 1.7976931348623157e+308 -- maior valor positivo double
    }
    ReplicatedStorage:WaitForChild("rEvents"):WaitForChild("zenMasterEvent"):FireServer(unpack(args))
end)

-- Submit número digitado
submitButton.MouseButton1Click:Connect(function()
    local num = tonumber(numberEntry.Text)
    if num and num > 0 and num <= 1.7976931348623157e+308 then
        ReplicatedStorage:WaitForChild("rEvents"):WaitForChild("zenMasterEvent"):FireServer("convertGems", num)
    else
        numberEntry.Text = "Número inválido!"
    end
end)

-- Discord clipboard
discordButton.MouseButton1Click:Connect(function()
    setclipboard("https://discord.gg/notexttospeech")
end)

-- Toggle Master Elements GUI
local masterGui = Instance.new("ScreenGui")
masterGui.Name = "MasterElementsGui"
masterGui.Parent = PlayerGui
masterGui.Enabled = false

local masterFrame = Instance.new("Frame")
masterFrame.Size = UDim2.new(0, 260, 0, 420)
masterFrame.Position = UDim2.new(0.3, 0, 0.25, 0)
masterFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
masterFrame.BorderSizePixel = 0
masterFrame.Active = true
masterFrame.Draggable = true
masterFrame.Parent = masterGui

local masterTitle = Instance.new("TextLabel")
masterTitle.Size = UDim2.new(1, 0, 0, 35)
masterTitle.BackgroundColor3 = Color3.fromRGB(50, 50, 65)
masterTitle.BorderSizePixel = 0
masterTitle.Text = "Master Elements"
masterTitle.TextColor3 = Color3.fromRGB(230, 230, 230)
masterTitle.Font = Enum.Font.GothamBold
masterTitle.TextSize = 18
masterTitle.Parent = masterFrame

local scrollFrame = Instance.new("ScrollingFrame")
scrollFrame.Size = UDim2.new(1, 0, 1, -35)
scrollFrame.Position = UDim2.new(0, 0, 0, 35)
scrollFrame.BackgroundTransparency = 1
scrollFrame.ScrollBarThickness = 6
scrollFrame.CanvasSize = UDim2.new(0, 0, 0, 370)
scrollFrame.Parent = masterFrame

local elements = {
    "Shadow Charge",
    "Electral Chaos",
    "Blazing Entity",
    "Shadowfire",
    "Lightning",
    "Masterful Wrath",
    "Inferno",
    "Eternity Storm",
    "Frost"
}

for i, element in ipairs(elements) do
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(1, -20, 0, 35)
    button.Position = UDim2.new(0, 10, 0, (i - 1) * 40)
    button.BackgroundColor3 = Color3.fromRGB(98, 102, 129)
    button.BorderSizePixel = 0
    button.Text = "Master " .. element
    button.TextColor3 = Color3.fromRGB(230, 230, 230)
    button.Font = Enum.Font.Gotham
    button.TextSize = 14
    button.Parent = scrollFrame

    button.MouseButton1Click:Connect(function()
        ReplicatedStorage:WaitForChild("rEvents"):WaitForChild("elementMasteryEvent"):FireServer(element)
    end)
end

toggleButton.MouseButton1Click:Connect(function()
    masterGui.Enabled = not masterGui.Enabled
end)

-- Variáveis para pulo infinito e corrida rápida
local infiniteJumpEnabled = false
local speedEnabled = false

-- Função Pulo Infinito
jumpButton.MouseButton1Click:Connect(function()
    infiniteJumpEnabled = not infiniteJumpEnabled
    jumpButton.Text = infiniteJumpEnabled and "Pulo Infinito: ON" or "Pulo Infinito: OFF"
end)

-- Evento para pulo infinito
game:GetService("UserInputService").JumpRequest:Connect(function()
    if infiniteJumpEnabled then
        local character = LocalPlayer.Character
        if character and character:FindFirstChildOfClass("Humanoid") then
            character.Humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
        end
    end
end)

-- Função Correr Rápido
speedButton.MouseButton1Click:Connect(function()
    speedEnabled = not speedEnabled
    speedButton.Text = speedEnabled and "Correr Rápido: ON" or "Correr Rápido: OFF"
    local character = LocalPlayer.Character
    if character and character:FindFirstChildOfClass("Humanoid") then
        if speedEnabled then
            character.Humanoid.WalkSpeed = 50 -- velocidade rápida
        else
            character.Humanoid.WalkSpeed = 16 -- padrão normal
        end
    end
end)

-- Botão fechar GUI
closeButton.MouseButton1Click:Connect(function()
    gui2.Enabled = false
end)

-- Botão minimizar GUI (esconder frame)
minimizeButton.MouseButton1Click:Connect(function()
    gui2Frame.Visible = not gui2Frame.Visible
end)
