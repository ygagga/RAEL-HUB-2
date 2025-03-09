-- Carregar a Redz Library
local success, Library = pcall(function()
    return loadstring(game:HttpGet("https://raw.githubusercontent.com/hacked-prototype/RedzLibV4/main/Source.lua"))()
end)

if not success or not Library then
    warn("Falha ao carregar a biblioteca.")
    return
end

if Library.SetTheme then Library:SetTheme("Dark") end
if Library.SetTransparency then Library:SetTransparency(0.1) end

-- Criar a janela
local Window = Library:MakeWindow({
    Title = "Redz Hub",
    SubTitle = "ESP Hack",
    LoadText = "Carregando...",
    Flags = "redz_hub"
})

-- Criar a aba Hackers
local HackersTab = Window:MakeTab({
    Title = "👾 Hackers",
    Flags = "hackers"
})

-- Variável de controle do ESP
local ESPAtivo = false

-- Função para ativar/desativar o ESP
local function ToggleESP(State)
    ESPAtivo = State

    if ESPAtivo then
        for _, player in pairs(game:GetService("Players"):GetPlayers()) do
            if player ~= game.Players.LocalPlayer and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                local highlight = Instance.new("Highlight", player.Character)
                highlight.FillColor = Color3.fromRGB(255, 255, 255) -- Branco
                highlight.FillTransparency = 0.3
                highlight.OutlineColor = Color3.fromRGB(255, 255, 255)
                highlight.OutlineTransparency = 0
            end
        end
    else
        for _, player in pairs(game:GetService("Players"):GetPlayers()) do
            if player.Character and player.Character:FindFirstChild("Highlight") then
                player.Character.Highlight:Destroy()
            end
        end
    end
end

-- Criar o Toggle para ativar/desativar o ESP
HackersTab:MakeToggle({
    Text = "Ativar ESP 👀",
    Flags = "esp_toggle",
    Default = false,
    Callback = function(Value)
        ToggleESP(Value)
    end
})

print("ESP Hack carregado com sucesso!")
