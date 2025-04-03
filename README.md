## #2

Сокращенные обозначения коммитов:

 - A — «install ant design»
 - B — «add support alias path»

Задачи:

 1. Из коммита **А** извлечь изменение с установкой _"@types/node": "20.1.3"_ и перенести его в коммит **B** (с помощью интерактивного rebase).

		git rebase 3d18078 -i =>
			edit 91e7052 install ant design
			edit 19523d4 add support alias path
			
		удалил изменение с установкой "@types/node": "20.1.3" из package.json
		
		git add .
		
		git commit --amend --no-edit
		
		git rebase --continue
	
		вернул изменение с установкой "@types/node": "20.1.3" в package.json
		
		git add .
		
		git commit --amend --no-edit
		
		git rebase --continue

 2. Коммит **B** переместить при помощи _git cherry-pick_ в ветку _development_.
 
		 git checkout development
		 
		 git cherry-pick d0754cf
		 
 3. Обновить ветку _feature/add-ant-design_ по _development_ (с помощью _git rebase_).
 
		 git checkout feature/add-ant-design
		 
		 git rebase development
 
 4. Влить ветку _feature/add-ant-design_ в _development_.
 
		git checkout development
		
		git merge feature/add-ant-design

## #3

Влить оставшиеся ветки (_feature/core_, _feature/calculator_, _feature/calculator-actions_) в _development_. Перед слиянием необходимо обновлять ветки по _development_ с помощью _git rebase_.

	git checkout feature/core

	git rebase development

	git checkout development

	git merge feature/core



	git checkout feature/calculator

	git rebase development

	разрезолвил конфликты в package.json и package-lock.json, приняв текущие изменения

	git add .

	git rebase --continue

	git checkout development

	git merge feature/calculator



	git checkout feature/calculator-actions

	git rebase development

	git checkout development

	git merge feature/calculator-actions

## #4

Применить патчи в приложение.

	переименовал патчи в соответствии с порядком применения, т.к. неверный порядок создает ошибку

	git am ./patches/*

### Переименование коммитов, обновление development по main, слияние development с main

	git rebase 3d18078 -i =>
		reword для всех коммитов =>
		переименовал коммиты в соответствии с Conventional Commits

	git rebase main

	разрезолвил конфликты в package.json и package-lock.json, приняв входящие изменения

	git add .

	git rebase --continue

	переименовал коммит с именем "fix package.json" в соответствии с Conventional Commits

	git checkout main

	git merge development

## #5

Создать репозиторий на GitHub или GitLab и загрузить в него локальный репозиторий. Выпустить релиз приложения в соответствии спецификацией SemVer.

	git tag 1.0.0
	
	git push --tags

	Create a new release => 
	Choose a tag => 
	Release title - 1.0.0 => 
	Release description - Выпустил релиз приложения в соответствии со спецификацией SemVer =>
	Generate release notes =>
	Publish release
