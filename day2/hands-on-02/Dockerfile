# 第一階段：建構階段
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

WORKDIR /app

# 複製專案文件並還原依賴
COPY MyApp.csproj .
RUN dotnet restore

# 複製其他文件並且進行編譯
COPY . .
RUN dotnet publish -c Release -o out

# 第二階段：運行階段
FROM mcr.microsoft.com/dotnet/runtime:8.0 AS runtime
WORKDIR /app
# 建構階段複製文件到運行階段
COPY --from=build /app/out .
ENTRYPOINT ["dotnet", "MyApp.dll"]