-- LocalScript para painel administrativo de spawn de armas e carros
-- Coloque este script em StarterPlayerScripts ou StarterGui

local armas = {"Parafal", "uzi", "ia2", "g2", "ar15"}
local carros = {
    "F1 Ferrari",
    "f1 Mercedes",
    "Ferrari Purosangue",
    "cybertruck",
    "Lamborghini Urus",
    "Dodge Charger"
}

-- Função para criar botões de spawn
local function criarBotao(nome, parent, onClick)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1, 0, 0, 30)
    btn.Text = nome
    btn.Parent = parent
    btn.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.MouseButton1Click:Connect(function()
        onClick(nome)
    end)
end

-- Cria o painel principal
local player = game.Players.LocalPlayer
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "AdminPanel"
screenGui.Parent = player:WaitForChild("PlayerGui")

local painel = Instance.new("Frame", screenGui)
painel.Size = UDim2.new(0, 300, 0, 400)
painel.Position = UDim2.new(0, 30, 0.5, -200)
painel.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
painel.BorderSizePixel = 0

-- Título
local titulo = Instance.new("TextLabel", painel)
titulo.Size = UDim2.new(1, 0, 0, 40)
titulo.Text = "Painel Admin (Spawn)"
titulo.BackgroundTransparency = 1
titulo.TextColor3 = Color3.fromRGB(255, 255, 127)
titulo.Font = Enum.Font.SourceSansBold
titulo.TextSize = 24

-- Seção armas
local armasLabel = Instance.new("TextLabel", painel)
armasLabel.Position = UDim2.new(0, 0, 0, 50)
armasLabel.Size = UDim2.new(1, 0, 0, 25)
armasLabel.Text = "Armas"
armasLabel.BackgroundTransparency = 1
armasLabel.TextColor3 = Color3.fromRGB(200, 200, 200)
armasLabel.Font = Enum.Font.SourceSans
armasLabel.TextSize = 18

local armasFrame = Instance.new("Frame", painel)
armasFrame.Position = UDim2.new(0, 10, 0, 80)
armasFrame.Size = UDim2.new(1, -20, 0, #armas * 35)
armasFrame.BackgroundTransparency = 1

for i, arma in ipairs(armas) do
    criarBotao(arma, armasFrame, function(nome)
        -- Adapte para o seu sistema de spawn de arma
        game.ReplicatedStorage.SpawnArma:FireServer(nome)
    end)
    armasFrame:GetChildren()[i].Position = UDim2.new(0, 0, 0, (i - 1) * 35)
end

-- Seção carros
local carrosLabel = Instance.new("TextLabel", painel)
carrosLabel.Position = UDim2.new(0, 0, 0, 110 + #armas * 35)
carrosLabel.Size = UDim2.new(1, 0, 0, 25)
carrosLabel.Text = "Carros"
carrosLabel.BackgroundTransparency = 1
carrosLabel.TextColor3 = Color3.fromRGB(200, 200, 200)
carrosLabel.Font = Enum.Font.SourceSans
carrosLabel.TextSize = 18

local carrosFrame = Instance.new("Frame", painel)
carrosFrame.Position = UDim2.new(0, 10, 0, 140 + #armas * 35)
carrosFrame.Size = UDim2.new(1, -20, 0, #carros * 35)
carrosFrame.BackgroundTransparency = 1

for i, carro in ipairs(carros) do
    criarBotao(carro, carrosFrame, function(nome)
        -- Adapte para o seu sistema de spawn de carro
        game.ReplicatedStorage.SpawnCarro:FireServer(nome)
    end)
    carrosFrame:GetChildren()[i].Position = UDim2.new(0, 0, 0, (i - 1) * 35)
end

-- Botão para fechar o painel
local fecharBtn = Instance.new("TextButton", painel)
fecharBtn.Size = UDim2.new(0, 60, 0, 30)
fecharBtn.Position = UDim2.new(1, -70, 0, 10)
fecharBtn.Text = "Fechar"
fecharBtn.BackgroundColor3 = Color3.fromRGB(120, 30, 30)
fecharBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
fecharBtn.MouseButton1Click:Connect(function()
    screenGui:Destroy()
end)
