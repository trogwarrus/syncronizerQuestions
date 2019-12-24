# Вопросы по синхронизатору 

```
материалы
https://wi.sbis.ru/doc/platform/application-debugging/js/doc-wasaby-dev-tools/
https://wi.sbis.ru/doc/platform/developmentapl/interface-development/ui-library/options
```

1. Синхронизация по сути является?
	+ `перерисовкой элементов на странице`
	- обновлением shadow-DOM
	- обновлением Virtual-DOM
	- обмен данными с БЛ

---
2. Возможный путь отладки синхронизации?
	- Процесс синхронизации - черный ящик и отладке не подлежит
	- С помощью расширения SBIS LOGS
	+ `С помощью расширения Wasaby Developer Tools`
	- Создать задачу на ответсвенного за синхронизатор

---
3. Что является сигналом к началу синхронизации !!!
	+ `изменение опции`
	- изменение реактивного свойства
	- вызов _startSync()
	- вызов _forceUpdate()
  
---
4. Для синхронизации опций не используются 
	+ `реактивные свойства`
	- биндинги
	+ `алиасы`
	+ `нативные функции браузера`
  
---	
5. Какие види биндингов существуют
	- в синхронизаторе биндинги не используются
	+ `одностороние`
	+ `двустороние`
	- скрытые 

---
6. Обратный биндинг - это другое название
	- одностороннего биндинга
	- синхронизатора
	- алиаса
	+ `двустороннего биндинга`
	- скрытого биндинга

---
7. Опции, переданные в _beforeMount будут доступны только для чтения в случае
	+ `одностороннего биндинга`
	- скрытого биндинга
	- двустороннего биндинга
	- опции всегда доступны для чтения и записи
  
---
8. Выберите правильный вариант настройки синхронизации опций _text после вызова _changeText()
	 - `Example.wml`
		 ```HTML
		<div>
			<div>
				{{ _text }}
			</div>
			<div on:click="_changeText()">
				Сменить текст
			</div>
			<Children text="{{ _text }}"/>
		</div>
		```
		Example.ts
		```TypeScript
		import { Control, TemplateFunction, IControlOptions } from 'UI/Base';
		import template = require('wml!Example');

		class Example {
			public _template: TemplateFunction = template;
			private _text: string;

			public _beforeMount() {
				this._text = 'Mounted';
			};

			public _changeText() {
				this._text = 'Changed';
			};
		}
		export = Example;
		```
		Children.wml
		```HTML
		<div>
			{{ _options.text }}
		</div>
		```
		Children.ts
		```TypeScript
		import { Control, TemplateFunction, IControlOptions } from 'UI/Base';
		import template = require('wml!Children');

		class Children extends Control<IControlOptions> {
		   public _template: TemplateFunction = template;
		}
		export = Children;
		```
	 - Example.wml
		 ```HTML
		<div>
			<div>
				{{ _text }}
			</div>
			<div on:click="_changeText()">
				Сменить текст
			</div>
			<Children _text="{{ _text }}"/>
		</div>
		```
		Example.ts
		```TypeScript
		import { Control, TemplateFunction, IControlOptions } from 'UI/Base';
		import template = require('wml!Example');

		class Example {
			public _template: TemplateFunction = template;
			private _text: string;

			public _beforeMount() {
				this._text = 'Mounted';
			};

			public _changeText() {
				this._text = 'Changed';
			};
		}
		export = Example;
		```
		Children.wml
		```HTML
		<div>
			{{ _options.text }}
		</div>
		```
		Children.ts
		```TypeScript
		import { Control, TemplateFunction, IControlOptions } from 'UI/Base';
		import template = require('wml!Children');

		class Children extends Control<IControlOptions> {
		   public _template: TemplateFunction = template;
		}
		export = Children;
		```
	 - Example.wml
		 ```HTML
		<div>
			<div>
				{{ _text }}
			</div>
			<div on:click="_changeText()">
				Сменить текст
			</div>
			<Children _text="{{ _text }}"/>
		</div>
		```
		Example.ts
		```TypeScript
		import { Control, TemplateFunction, IControlOptions } from 'UI/Base';
		import template = require('wml!Example');

		class Example {
			public _template: TemplateFunction = template;
			private _text: string;

			public _beforeMount() {
				this._text = 'Mounted';
			};

			public _changeText() {
				this._text = 'Changed';
			};
		}
		export = Example;
		```
		Children.wml
		```HTML
		<div>
			{{ _options._text }}
		</div>
		```
		Children.ts
		```TypeScript
		import { Control, TemplateFunction, IControlOptions } from 'UI/Base';
		import template = require('wml!Children');

		class Children extends Control<IControlOptions> {
		   public _template: TemplateFunction = template;
		}
		export = Children;
		```
	 - Example.wml
		 ```HTML
		<div>
			<div>
				{{ _text }}
			</div>
			<div on:click="_changeText()">
				Сменить текст
			</div>
			<Children text="{{ _text }}"/>
		</div>
		```
		Example.ts
		```TypeScript
		import { Control, TemplateFunction, IControlOptions } from 'UI/Base';
		import template = require('wml!Example');

		class Example {
			public _template: TemplateFunction = template;
			private _text: string;

			public _beforeMount() {
				this._text = 'Mounted';
			};

			public _changeText() {
				this._text = 'Changed';
			};
		}
		export = Example;
		```
		Children.wml
		```HTML
		<div>
			{{ options.text }}
		</div>
		```
		Children.ts
		```TypeScript
		import { Control, TemplateFunction, IControlOptions } from 'UI/Base';
		import template = require('wml!Children');

		class Children extends Control<IControlOptions> {
		   public _template: TemplateFunction = template;
		}
		export = Children;
		```

---
9. В каком файле допущена ошибка при реализации синхронизации
 	- Example.wml
		 ```HTML
		<div>
			<div>
				{{ _text }}
			</div>
			<div on:click="_changeText()">
				Сменить текст
			</div>
			<Children text="{{ _text }}"/>
		</div>
		```
	- Example.ts
		```TypeScript
		import { Control, TemplateFunction, IControlOptions } from 'UI/Base';
		import template = require('wml!Example');

		class Example {
			public _template: TemplateFunction = template;
			private _text: string;

			public _beforeMount() {
				this._text = 'Mounted';
			};

			public _changeText() {
				this._text = 'Changed';
			};
		}
		export = Example;
		```
	- `Children.wml`
		```HTML
		<div>
			{{ options.text }}
		</div>
		```
	- Children.ts
		```TypeScript
		import { Control, TemplateFunction, IControlOptions } from 'UI/Base';
		import template = require('wml!Children');

		class Children extends Control<IControlOptions> {
		   public _template: TemplateFunction = template;
		}
		export = Children;
		```
---
10. Какая запись является верной
	- < Example bind:variable='_options.variable' />
	- `< Example bind:variable='_variable' />`
	- < Example binds:variable='_options.variable' />
	- < Example binds:variable='_variable' /> 
	- `< Example bind:variable='_options.record._variable' />`

---
11. На что можно ссылаться при обратном биндинге
	- `на свойство объекта, лежащего в опциях`
	- `на примитив, объявленный на инстансе`
	- на объект, объявленный на инстансе
	- нет ограничений, ссылаться можно абсолютно на все
	
---
12. Выберите правильный вариант использования двухсторонней синхронизации опций, если
	Example.wml
	```HTML
	<div>
		<div>
			{{ _text }}
		</div>
		<div on:click="_changeText()">
			Сменить текст
		</div>
		<Children bind:text="_text"/>
	</div>
	```
	Example.ts
	```TypeScript
	import { Control, TemplateFunction, IControlOptions } from 'UI/Base';
	import template = require('wml!Example');

	class Example extends Control<IControlOptions> {
	   public _template: TemplateFunction = template;
	   private _text: string;

	   public _beforeMount() {
		 this._text = 'Mounted';
	   };

	   public _changeText() {
		  this._text = 'Changed';
	   };
	}

	export = Example;
	```
	
	- Children.wml
		```HTML
		<div>
			<div>
				{{ _options.text }}
			</div>
			<div bind:click="_revertText()">
				Вернуть текст
			</div>
		</div>

		```
		Children.ts
		```TypeScript
		import { Control, TemplateFunction, IControlOptions } from 'UI/Base';
		import template = require('wml!Children');

		class Children extends Control<IControlOptions> {
		   public _template: TemplateFunction = template;

		   public _revertText() {
			  this._notify('textChanged', ['Reverted']);
		   };
		}

		export = Children;
		```
	- Children.wml
		```HTML
		<div>
			<div>
				{{ _options.text }}
			</div>
			<div on:click="_revertText()">
				Вернуть текст
			</div>
		</div>

		```
		Children.ts
		```TypeScript
		import { Control, TemplateFunction, IControlOptions } from 'UI/Base';
		import template = require('wml!Children');

		class Children extends Control<IControlOptions> {
		   public _template: TemplateFunction = template;

		   public _revertText() {
			  this._notify('click', ['Reverted']);
		   };
		}

		export = Children;
		```
	- `Children.wml`
		```HTML
		<div>
			<div>
				{{ _options.text }}
			</div>
			<div on:click="_revertText()">
				Вернуть текст
			</div>
		</div>

		```
		Children.ts
		```TypeScript
		import { Control, TemplateFunction, IControlOptions } from 'UI/Base';
		import template = require('wml!Children');

		class Children extends Control<IControlOptions> {
		   public _template: TemplateFunction = template;

		   public _revertText() {
			  this._notify('textChanged', ['Reverted']);
		   };
		}

		export = Children;
		```
	- Children.wml
		```HTML
		<div>
			<div>
				{{ _options.text }}
			</div>
			<div on:click="_revertText()">
				Вернуть текст
			</div>
		</div>

		```
		Children.ts
		```TypeScript
		import { Control, TemplateFunction, IControlOptions } from 'UI/Base';
		import template = require('wml!Children');

		class Children extends Control<IControlOptions> {
		   public _template: TemplateFunction = template;

		   public _revertText() {
			  this._bind('click', ['Reverted']);
		   };
		}

		export = Children;
		```
---
13. В каком файле допущена ошибка при реализации синхронизации
	- `Exapmle.wml`
		```HTML
		<div>
			<div>
				{{ _text }}
			</div>
			<div on:click="_changeText()">
				Сменить текст
			</div>
			<Children bind:text="{{_text}}"/>
		</div>
		```
	- Exapmle.ts
		```TypeScript
		import { Control, TemplateFunction, IControlOptions } from 'UI/Base';
		import template = require('wml!Example');

		class Example extends Control<IControlOptions> {
		   public _template: TemplateFunction = template;
		   private _text: string;

		   public _beforeMount() {
			 this._text = 'Mounted';
		   };

		   public _changeText() {
			  this._text = 'Changed';
		   };
		}

		export = Example;
		```
	- Children.wml
		```HTML
		<div>	
			<div>
				{{ _options.text }}
			</div>
			<div on:click="_revertText()">
				Вернуть текст
			</div>
		</div>
		```
	- `Children.ts`
		```TypeScript
		import { Control, TemplateFunction, IControlOptions } from 'UI/Base';
		import template = require('wml!Children');

		class Children extends Control<IControlOptions> {
		   public _template: TemplateFunction = template;

		   public _revertText() {
			  this._bind('textChanged', ['Reverted']);
		   };
		}

		export = Children;
		```
---
14. Какие элементы будут синхронизированы после выполнения _startSync() 
	Example.wml
	```HTML
	<div>	
		<div>
			{{ _text }}
		</div>
		<div on:click="_changeText()">
			Сменить текст
		</div>
		<Children bind:text="_text"/>
	</div>

	```

---
15.
