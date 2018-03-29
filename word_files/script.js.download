'use strict';


var kite = {browser : {}};

var nbe = {
	browser : {icon : {}},
	dynamic : {},
	css : {},
	site : {},
	lib : {},
	doc : {},
	state : {},
	inputs : {},
	notify : {},
	format : {},
	location : {},
	events : {},
	triggers : {},
	ops : {},
	editor : {},
	paste : {},
	title : {},
	publish : {}
};


// console.log

(function () {
	if (typeof console === "undefined") {
		console = {};
	}
	if (typeof console.log === "undefined") {
		console.log = function () {};
	}
}());

// classList
if (typeof document !== "undefined" && !("classList" in document.createElement("a"))) {
	(function (view) {
		var classListProp, protoProp, elemCtrProto, objCtr, strTrim, arrIndexOf, DOMEx, checkTokenAndGetIndex, ClassList, classListProto, classListGetter, classListPropDesc;

		classListProp = "classList";
		protoProp = "prototype";
		elemCtrProto = (view.HTMLElement || view.Element)[protoProp];
		objCtr = Object;
		strTrim = String[protoProp].trim || function () {
			return this.replace(/^\s+|\s+$/g, "");
		};
		arrIndexOf = Array[protoProp].indexOf || function (item) {
			var i, len;

			len = this.length;

			for (i = 0; i < len; i++) {
				if (i in this && this[i] === item) {
					return i;
				}
			}
			return -1;
		};
		// Vendors: please allow content code to instantiate DOMExceptions
		DOMEx = function (type, message) {
			this.name = type;
			this.code = DOMException[type];
			this.message = message;
		};
		checkTokenAndGetIndex = function (classList, token) {
			if (token === "") {
				throw new DOMEx(
					"SYNTAX_ERR",
					"An invalid or illegal string was specified"
				);
			}
			if (/\s/.test(token)) {
				throw new DOMEx(
					"INVALID_CHARACTER_ERR",
					"String contains an invalid character"
				);
			}
			return arrIndexOf.call(classList, token);
		};
		ClassList = function (elem) {
			var trimmedClasses, classes, i, len;

			trimmedClasses = strTrim.call(elem.className);
			classes = trimmedClasses ? trimmedClasses.split(/\s+/) : [];
			len = classes.length;

			for (i = 0; i < len; i++) {
				this.push(classes[i]);
			}
			this._updateClassName = function () {
				elem.className = this.toString();
			};
		};
		classListProto = ClassList[protoProp] = [];
		classListGetter = function () {
			return new ClassList(this);
		};

		// Most DOMException implementations don't allow calling DOMException's toString()
		// on non-DOMExceptions. Error's toString() is sufficient here.
		DOMEx[protoProp] = Error[protoProp];
		classListProto.item = function (i) {
			return this[i] || null;
		};
		classListProto.contains = function (token) {
			token += "";
			return checkTokenAndGetIndex(this, token) !== -1;
		};
		classListProto.add = function (token) {
			token += "";
			if (checkTokenAndGetIndex(this, token) === -1) {
				this.push(token);
				this._updateClassName();
			}
		};
		classListProto.remove = function (token) {
			var index;

			token += "";
			index = checkTokenAndGetIndex(this, token);
			if (index !== -1) {
				this.splice(index, 1);
				this._updateClassName();
			}
		};
		classListProto.toggle = function (token) {
			token += "";
			if (checkTokenAndGetIndex(this, token) === -1) {
				this.add(token);
			} else {
				this.remove(token);
			}
		};
		classListProto.toString = function () {
			return this.join(" ");
		};

		if (objCtr.defineProperty) {
			classListPropDesc = {
				get: classListGetter,
				enumerable: true,
				configurable: true
			};
			try {
				objCtr.defineProperty(elemCtrProto, classListProp, classListPropDesc);
			} catch (ex) { // IE 8 doesn't support enumerable:true
				if (ex.number === -0x7FF5EC54) {
					classListPropDesc.enumerable = false;
					objCtr.defineProperty(elemCtrProto, classListProp, classListPropDesc);
				}
			}
		} else if (objCtr[protoProp].__defineGetter__) {
			elemCtrProto.__defineGetter__(classListProp, classListGetter);
		}
	}(window.self));
}

// addEventListener
if (window.Element && !window.addEventListener) {
	var attach, remove;

	attach = function (type, listener, useCapture) {
		this.attachEvent('on' + type, function () {
			var event;

			event = window.event;
			event.target = event.srcElement;

			listener(event);
		});
	};

	remove = function (type, listener, useCapture) {
		this.detachEvent('on' + type, listener);
	};

	window.Element.prototype.addEventListener = attach;
	window.Element.prototype.removeEventListener = remove;
	Window.prototype.addEventListener = attach;
	Window.prototype.removeEventListener = remove;
	document.addEventListener = attach;
	document.removeEventListener = remove;
}

/*
// Shim for DOM Events
// http://www.quirksmode.org/blog/archives/2005/10/_and_the_winner_1.html
// Use addEvent(object, event, handler) instead of object.addEventListener(event, handler)
window.addEvent = function (obj, type, fn) {
	if (obj.addEventListener) {
		obj.addEventListener(type, fn, false);
	} else if (obj.attachEvent) {
		obj["e" + type + fn] = fn;
		obj[type + fn] = function () {
			var e = window.event;
			e.currentTarget = obj;
			e.preventDefault = function () { e.returnValue = false; };
			e.stopPropagation = function () { e.cancelBubble = true; };
			e.target = e.srcElement;
			e.timeStamp = new Date();
			obj["e" + type + fn].call(this, e);
		};
		obj.attachEvent("on" + type, obj[type + fn]);
	}
};

window.removeEvent = function (obj, type, fn) {
	if (obj.removeEventListener) {
		obj.removeEventListener(type, fn, false);
	} else if (obj.detachEvent) {
		obj.detachEvent("on" + type, obj[type + fn]);
		obj[type + fn] = null;
		obj["e" + type + fn] = null;
	}
};
*/

// Object.keys
if (!Object.keys) {
	Object.keys = (function () {
		var hop, hasDontEnumBug, dontEnums, dontEnumsLength;

		hop = Object.prototype.hasOwnProperty;
		hasDontEnumBug = !({toString: null}).propertyIsEnumerable('toString');
		dontEnums = [
			'toString',
			'toLocaleString',
			'valueOf',
			'hasOwnProperty',
			'isPrototypeOf',
			'propertyIsEnumerable',
			'constructor'
		];
		dontEnumsLength = dontEnums.length;

		return function (obj) {
			var result, prop, i;

			if (typeof obj !== 'object' && typeof obj !== 'function' || obj === null) {
				throw new TypeError('Object.keys called on non-object');
			}

			result = [];

			for (prop in obj) {
				if (hop.call(obj, prop)) {
					result.push(prop);
				}
			}

			if (hasDontEnumBug) {
				for (i = 0; i < dontEnumsLength; i++) {
					if (hop.call(obj, dontEnums[i])) {
						result.push(dontEnums[i]);
					}
				}
			}
			return result;
		};
	}());
}

// Production steps of ECMA-262, Edition 5, 15.4.4.19
// Reference: http://es5.github.com/#x15.4.4.19
if (!Array.prototype.map) {
	Array.prototype.map = function (callback, thisArg) {
		var T, A, k, O, len, kValue, mappedValue;

		if (this === null) {
			throw new TypeError(" this is null or not defined");
		}

		// 1. Let O be the result of calling ToObject passing the |this| value as the argument.
		//O = Object(this);
		O = {};

		// 2. Let lenValue be the result of calling the Get internal method of O with the argument "length".
		// 3. Let len be ToUint32(lenValue).
		//len = O.length >>> 0;
		len = O.length > 0;

		// 4. If IsCallable(callback) is false, throw a TypeError exception.
		// See: http://es5.github.com/#x9.11
		if ({}.toString.call(callback) !== "[object Function]") {
			throw new TypeError(callback + " is not a function");
		}

		// 5. If thisArg was supplied, let T be thisArg; else let T be undefined.
		if (thisArg) {
			T = thisArg;
		}

		// 6. Let A be a new array created as if by the expression new Array(len) where Array is
		// the standard built-in constructor with that name and len is the value of len.
		A = new Array(len);

		// 7. Let k be 0
		k = 0;

		// 8. Repeat, while k < len
		while (k < len) {
			// a. Let Pk be ToString(k).
			//	 This is implicit for LHS operands of the in operator
			// b. Let kPresent be the result of calling the HasProperty internal method of O with argument Pk.
			//	 This step can be combined with c
			// c. If kPresent is true, then
			if (k in O) {

				// i. Let kValue be the result of calling the Get internal method of O with argument Pk.
				kValue = O[k];

				// ii. Let mappedValue be the result of calling the Call internal method of callback
				// with T as the this value and argument list containing kValue, k, and O.
				mappedValue = callback.call(T, kValue, k, O);

				// iii. Call the DefineOwnProperty internal method of A with arguments
				// Pk, Property Descriptor {Value: mappedValue, Writable: true, Enumerable: true, Configurable: true},
				// and false.

				// In browsers that support Object.defineProperty, use the following:
				// Object.defineProperty(A, Pk, { value: mappedValue, writable: true, enumerable: true, configurable: true });

				// For best browser support, use the following:
				A[k] = mappedValue;
			}
			// d. Increase k by 1.
			k++;
		}

		// 9. return A
		return A;
	};
}

// Date.now()
Date.now = Date.now || function () {
	return +new Date();
};

// Array indexOf()
if (!Array.prototype.indexOf) {
	Array.prototype.indexOf = function (searchElement /*, fromIndex */ ) {
		var t, len, n, k;

		if (this === null) {
			throw new TypeError();
		}
		//t = Object(this);
		t = {};
		//len = t.length >>> 0;
		len = t.length > 0;
		if (len === 0) {
			return -1;
		}
		n = 0;
		if (arguments.length > 0) {
			n = Number(arguments[1]);
			if (n !== n) { // shortcut for verifying if it's NaN
				n = 0;
			} else if (n !== 0 && n !== Infinity && n !== -Infinity) {
				n = (n > 0 || -1) * Math.floor(Math.abs(n));
			}
		}
		if (n >= len) {
			return -1;
		}
		k = n >= 0 ? n : Math.max(len - Math.abs(n), 0);
		for (; k < len; k++) {
			if (k in t && t[k] === searchElement) {
				return k;
			}
		}
		return -1;
	};
}

// Array filter
if (!Array.prototype.filter) {
	Array.prototype.filter = function (fun /*, thisp */) {
		"use strict";
		var t, len, res, thisp, i, val;

		if (this === null) {
			throw new TypeError();
		}

		t = {};//Object(this)
		len = t.length > 0;
		if (typeof fun !== "function") {
			throw new TypeError();
		}

		res = [];
		thisp = arguments[1];
		for (i = 0; i < len; i++) {
			if (i in t) {
				val = t[i]; // in case fun mutates this
				if (fun.call(thisp, val, i, t)) {
					res.push(val);
				}
			}
		}

		return res;
	};
}
// Array foreach

if (!Array.prototype.forEach) {
	Array.prototype.forEach = function forEach(callback, thisArg) {
		var T, k, O, len, kValue;

		if (this === null) {
			throw new TypeError("this is null or not defined");
		}

		// 1. Let O be the result of calling ToObject passing the |this| value as the argument.
		O = {};//Object(this);

		// 2. Let lenValue be the result of calling the Get internal method of O with the argument "length".
		// 3. Let len be ToUint32(lenValue).
		len = O.length > 0; // Hack to convert O.length to a UInt32 >>>

		// 4. If IsCallable(callback) is false, throw a TypeError exception.
		// See: http://es5.github.com/#x9.11
		if ({}.toString.call(callback) !== "[object Function]") {
			throw new TypeError(callback + " is not a function");
		}

		// 5. If thisArg was supplied, let T be thisArg; else let T be undefined.
		if (thisArg) {
			T = thisArg;
		}

		// 6. Let k be 0
		k = 0;

		// 7. Repeat, while k < len
		while (k < len) {

			// a. Let Pk be ToString(k).
			//	 This is implicit for LHS operands of the in operator
			// b. Let kPresent be the result of calling the HasProperty internal method of O with argument Pk.
			//	 This step can be combined with c
			// c. If kPresent is true, then
			if (Object.prototype.hasOwnProperty.call(O, k)) {

				// i. Let kValue be the result of calling the Get internal method of O with argument Pk.
				kValue = O[k];

				// ii. Call the Call internal method of callback with T as the this value and
				// argument list containing kValue, k, and O.
				callback.call(T, kValue, k, O);
			}
			// d. Increase k by 1.
			k++;
		}
		// 8. return undefined
	};
}

nbe.site.panel = function (el_panel_container, editor) {
	var defval, left_margin_initial_value, is_visible, buttons, el_panel, toggle_panel, el_toggle_panel, el_font, font_family_spec, el_format, el_color, el_paragraph, el_insert, key, button_undo, el_hide_format_panel;

	defval = nbe.state.formats.default_values;
	left_margin_initial_value = 'off:on';
	is_visible = false;

	buttons = {};

	el_panel = kite.browser.dom.eac('div', el_panel_container, 'wu-format-panel');

	toggle_panel = function () {
		if (is_visible) {
			el_panel.className = 'wu-format-panel';
			el_toggle_panel.textContent = 'More';
		} else {
			el_panel.className = 'wu-format-panel open';
			el_toggle_panel.textContent = 'Less';
		}
		is_visible = !is_visible;
	};

	el_toggle_panel = kite.browser.dom.eac('button', el_panel_container, 'wu-toggle circle_button');
	el_toggle_panel.textContent = 'More';
	el_toggle_panel.addEventListener('click', toggle_panel, false);

	el_panel.addEventListener('click', function (e) {
		if (e.target.classList.contains('wu-icon') || e.target.parentNode.classList.contains('drop_down_menu') || e.target.parentNode.parentNode.classList.contains('drop_down_menu')) {
			toggle_panel();
		}
	}, false);

	el_font = kite.browser.dom.ea('div', el_panel);

	buttons.heading = nbe.inputs.heading(editor.trigger, 'Heading', {none : 'No heading (-)', heading1 : '<span class="line heading1">Heading 1 (H1)</span>', heading2 : '<span class="line heading2">Heading 2 (H2)</span>', heading3 : '<span class="line heading3">Heading 3 (H3)</span>', heading4 : '<span class="line heading4">Heading 4 (H4)</span>', heading5 : '<span class="line heading5">Heading 5 (H5)</span>', heading6 : '<span class="line heading6">Heading 6 (H6)</span>'}, {none : '-', heading1 : 'H1', heading2 : 'H2', heading3 : 'H3', heading4 : 'H4', heading5 : 'H5', heading6 : 'H6'}, el_font, defval.heading);

	font_family_spec = {};
	nbe.state.formats.font_family.forEach(function (family) {
		var family_upper;

		family_upper = family[0].toUpperCase() + family.slice(1);
		font_family_spec[family] = '<span style="font-family : ' + family_upper + ';">' + family_upper + '</span>';
	});

	buttons.font_family = nbe.inputs.font_family(editor.trigger, 'Font', font_family_spec, el_font, defval.font_family);

	buttons.font_size = nbe.inputs.font_size(editor.trigger, 'Font size', {'10px' : '10', '11px' : '11', '12px' : '12', '13px' : '13', '14px' : '14', '16px' : '16', '18px' : '18', '20px' : '20', '22px' : '22', '24px' : '24', '28px' : '28', '32px' : '32', '36px' : '36', '48px' : '48', '72px' : '72'}, el_font, defval.font_size);

	el_format = kite.browser.dom.ea('div', el_panel);
	buttons.bold = nbe.inputs.bold(editor.trigger, 'Bold', el_format, defval.bold);
	buttons.italic = nbe.inputs.italic(editor.trigger, 'Italic', el_format, defval.italic);
	buttons.underline = nbe.inputs.underline(editor.trigger, 'Underline', el_format, defval.underline);
	buttons.strikethrough = nbe.inputs.strikethrough(editor.trigger, 'Strikethrough', el_format, defval.strikethrough);

	el_color = kite.browser.dom.ea('div', el_panel);
	buttons.color = nbe.inputs.color(editor.trigger, 'Text color', el_color, defval.color);
	buttons.background_color = nbe.inputs.background_color(editor.trigger, 'Line color', el_color, defval.background_color);

	buttons.vertical_align = nbe.inputs.vertical_align(editor.trigger, kite.browser.dom.ea('div', el_panel), defval.vertical_align);

	buttons.left_margin = nbe.inputs.left_margin(editor.trigger, kite.browser.dom.ea('div', el_panel), left_margin_initial_value);

	el_paragraph = kite.browser.dom.ea('div', el_panel);
	buttons.text_align = nbe.inputs.text_align(editor.trigger, 'Text align', {left : 'Left', center : 'Center', right : 'Right', justify : 'Justify'}, el_paragraph, defval.text_align);
	buttons.line_spacing = nbe.inputs.line_spacing(editor.trigger, 'Line spacing', {'line_spacing_05' : '0.5', 'line_spacing_06' : '0.6', 'line_spacing_07' : '0.7', 'line_spacing_08' : '0.8', 'line_spacing_09' : '0.9', 'line_spacing_10' : '1', 'line_spacing_11' : '1.1', 'line_spacing_12' : '1.2', 'line_spacing_13' : '1.3', 'line_spacing_14' : '1.4', 'line_spacing_15' : '1.5', 'line_spacing_16' : '1.6 (default)', 'line_spacing_17' : '1.7', 'line_spacing_18' : '1.8', 'line_spacing_19' : '1.9', 'line_spacing_20' : '2'}, el_paragraph, defval.line_spacing);

	buttons.list = nbe.inputs.list(editor.trigger, 'List', {none : 'none', disc : '•', 'square' : '▀', ordered : '1. 2. 3.', 'lower-alpha' : 'a. b. c.', 'upper-alpha' : 'A. B. C.', 'lower-roman' : 'i. ii. iii.', 'upper-roman' : 'I. II. III.'}, kite.browser.dom.ea('div', el_panel), defval.list);

	el_insert = kite.browser.dom.ea('div', el_panel);
	buttons.special_characters = nbe.inputs.special_characters(editor.trigger, 'Special characters', el_insert, null);
	buttons.insert_link = nbe.inputs.insert_link(editor.trigger, 'Insert link', el_insert);
	buttons.edit_link = nbe.inputs.edit_link(editor.trigger, 'Edit link', el_insert, null);
	buttons.insert_img = nbe.inputs.insert_image(editor.trigger, 'Insert image', el_insert);
	buttons.edit_img = nbe.inputs.edit_image(editor.trigger, 'Edit image', el_insert, null);

	for (key in buttons) {
		if (buttons.hasOwnProperty(key)) {
			editor.inputs.add(key, buttons[key]);
		}
	}

	button_undo = nbe.inputs.undo(editor.trigger, kite.browser.dom.ea('div', el_panel));
	editor.undo.add_button(button_undo);

	el_hide_format_panel = kite.browser.dom.eac('button', el_panel, 'hide circle_button');
	el_hide_format_panel.textContent = 'Close';
	el_hide_format_panel.addEventListener('click', toggle_panel, false);
};


nbe.site.status_panel = function (ids) {
	var element, share, el_share_button, display_export, el_export_button, network, saved, set_status, display;

	element = kite.browser.dom.ec('div', 'status_panel');

	share = nbe.site.display_share(ids);

	el_share_button = kite.browser.dom.eac('button', element, 'circle_button');
	el_share_button.textContent = 'Share';
	el_share_button.addEventListener('click', function (e) {
		share.display(ids);
	}, false);

	display_export = nbe.site.display_export(ids);

	el_export_button = nbe.browser.icon.exporticon(element);
	el_export_button.addEventListener('click', function (e) {
		display_export.display();
	}, false);

	network = nbe.browser.icon.network(element);
	saved = nbe.browser.icon.saved(element);

	set_status = function (key, value) {
		if (key === 'network') {
			if (value === 'connected') {
				//el_network.title = 'You are online';
				network.on();
			} else {
				//el_network.title = 'You are offline';
				network.off();
			}
		} else if (key === 'nunsaved') {
			if (value > 0) {
				//el_saved.title = 'You have unsaved changes';
				saved.off();
			} else {
				//el_saved.title = 'You are offline';
				saved.on();
			}
		}
	};

	display = function (el_panel_container) {
		el_panel_container.appendChild(element);
	};

	return {set_status : set_status, display : display};
};


nbe.site.display_demo = function () {
	var doc, ops, editor_write, editor_read;

	doc = nbe.doc.create({id : 'demo', read : null, write : null, new_doc : true}, false, null, function (key, value) {});

	ops = [
                {domop : 'append', id : 'line2', parent : 'root', type : 'line', val : {}},
                {domop : 'append', id : 'line3', parent : 'root', type : 'line', val : {}},
                {domop : 'append', id : 'line4', parent : 'root', type : 'line', val : {}},
                {domop : 'append', id : 'line5', parent : 'root', type : 'line', val : {heading : 'heading4'}},
                {domop : 'append', id : 'line6', parent : 'root', type : 'line', val : {}},
                {domop : 'append', id : 'line7', parent : 'root', type : 'line', val : {}},
                {domop : 'append', id : 'line8', parent : 'root', type : 'line', val : {}},
                {domop : 'append', id : 'line9', parent : 'root', type : 'line', val : {list : 'ordered'}},
                {domop : 'append', id : 'line10', parent : 'root', type : 'line', val : {list : 'ordered'}},
                {domop : 'append', id : 'line11', parent : 'root', type : 'line', val : {list : 'ordered'}},
                {domop : 'append', id : 'line12', parent : 'root', type : 'line', val : {list : 'ordered'}},
                {domop : 'append', id : 'line13', parent : 'root', type : 'line', val : {list : 'ordered'}},
                {domop : 'append', id : 'line14', parent : 'root', type : 'line', val : {list : 'ordered'}},
                {domop : 'append', id : 'line15', parent : 'root', type : 'line', val : {list : 'ordered'}},
                {domop : 'append', id : 'line16', parent : 'root', type : 'line', val : {}},
                {domop : 'append', id : 'line17', parent : 'root', type : 'line', val : {text_align : 'center'}},
                {domop : 'append', id : 'line18', parent : 'root', type : 'line', val : {text_align : 'center'}},
                {domop : 'append', id : 'line19', parent : 'root', type : 'line', val : {text_align : 'center'}},
                {domop : 'append', id : 'line20', parent : 'root', type : 'line', val : {}},
                {domop : 'append', id : 'line21', parent : 'root', type : 'line', val : {}},
                {domop : 'append', id : 'line22', parent : 'root', type : 'line', val : {left_margin : 20}},
                {domop : 'append', id : 'line23', parent : 'root', type : 'line', val : {left_margin : 40}},
                {domop : 'append', id : 'line24', parent : 'root', type : 'line', val : {}},
                {domop : 'append', id : 'line25', parent : 'root', type : 'line', val : {}},
                {domop : 'append', id : 'line26', parent : 'root', type : 'line', val : {}},
                {domop : 'append', id : 'line27', parent : 'root', type : 'line', val : {}},
                {domop : 'append', id : 'line28', parent : 'root', type : 'line', val : {}},
                {domop : 'append', id : 'text1.2', parent : 'line', type : 'text', val : {text : 'Write in the left windows and see changes in the right window'}},
                {domop : 'append', id : 'text3.1', parent : 'line3', type : 'text', val : {text : 'You can insert '}},
                {domop : 'append', id : 'link3.2', parent : 'line3', type : 'link', val : {href : 'www.writeurl.com'}},
                {domop : 'append', id : 'text3.3', parent : 'link3.2', type : 'text', val : {text : 'links'}},
                {domop : 'append', id : 'text3.4', parent : 'line3', type : 'text', val : {text : ', images '}},
                {domop : 'append', id : 'img3.5', parent : 'line3', type : 'img', val : {src : '/img/nyckelpiga.jpg', height : '50'}},
                {domop : 'append', id : 'text3.6', parent : 'line3', type : 'text', val : {text : ' and special characters : \u03b1\u03b2\u03b3'}},
                {domop : 'append', id : 'text5.1', parent : 'line5', type : 'text', val : {text : 'Lines can have headers'}},
                {domop : 'append', id : 'text7.1', parent : 'line7', type : 'text', val : {text : 'There are lists and formatted text'}},
                {domop : 'append', id : 'text9.1', parent : 'line9', type : 'text', val : {text : 'bold', bold : 'on'}},
                {domop : 'append', id : 'text10.1', parent : 'line10', type : 'text', val : {text : 'italic', italic : 'on'}},
                {domop : 'append', id : 'text11.1', parent : 'line11', type : 'text', val : {text : 'underline', underline : 'on'}},
                {domop : 'append', id : 'text12.1', parent : 'line12', type : 'text', val : {text : 'strikethrough', strikethrough : 'on'}},
                {domop : 'append', id : 'text13.1', parent : 'line13', type : 'text', val : {text : 'color', color : 'rgb(255,0,0)'}},
                {domop : 'append', id : 'text14.1', parent : 'line14', type : 'text', val : {text : 'line color', background_color : 'rgb(255,255,0)'}},
                {domop : 'append', id : 'text15.1', parent : 'line15', type : 'text', val : {text : 'superscript', vertical_align : 'super'}},
                {domop : 'append', id : 'text15.2', parent : 'line15', type : 'text', val : {text : ' and '}},
                {domop : 'append', id : 'text15.3', parent : 'line15', type : 'text', val : {text : 'subscript', vertical_align : 'sub'}},
                {domop : 'append', id : 'text17.1', parent : 'line17', type : 'text', val : {text : 'Text alignments can be left,'}},
                {domop : 'append', id : 'text18.1', parent : 'line18', type : 'text', val : {text : 'center (as here),'}},
                {domop : 'append', id : 'text19.1', parent : 'line19', type : 'text', val : {text : 'right and justify.'}},
                {domop : 'append', id : 'text21.1', parent : 'line21', type : 'text', val : {text : 'Text can'}},
                {domop : 'append', id : 'text22.1', parent : 'line22', type : 'text', val : {text : 'also have'}},
                {domop : 'append', id : 'text23.1', parent : 'line23', type : 'text', val : {text : 'indentation levels'}},
                {domop : 'append', id : 'text25.1', parent : 'line25', type : 'text', val : {text : 'Undo ( button or ctrl-z), redo (button or ctrl-shift-z)'}},
                {domop : 'append', id : 'text26.1', parent : 'line26', type : 'text', val : {text : 'Copy (ctrl-c), cut (ctrl-x), paste (ctrl-v)'}},
                {domop : 'append', id : 'text28.1', parent : 'line28', type : 'text', val : {text : 'spell check, fonts, line spacing.'}}
        ];

	doc.add_ops(null, ops);

	editor_write = doc.editors.add('editor_write', 'text', {editable : true});
	document.getElementById('editor_write').appendChild(editor_write.el_editor);

	editor_read = doc.editors.add('editor_read', 'text', {editable : false});
	document.getElementById('editor_read').appendChild(editor_read.el_editor);

	nbe.site.panel(document.getElementById('demo_panel'), editor_write);
};


nbe.site.display_editor = function (doc) {
	var editable, editor, el_editor_container, title_editor;

	editable = doc.ids.write !== null;
	document.getElementById('frontpage').style.display = 'none';
	if (editable) {
		document.body.className = 'editor';
	} else {
		document.getElementById('home').style.display = 'none';
		document.getElementById('feedback').style.display = 'none';
		document.getElementById('faq').style.display = 'none';
		document.body.className = 'read_editor';
	}

	editor = doc.editors.add('editor', 'text', {editable : editable});
	el_editor_container = kite.browser.dom.eac('div', document.body, 'editor_container');

	if (editable) {
		nbe.site.panel(document.getElementById('panel'), editor);
	}

	title_editor = doc.editors.add('title_editor', 'title', {editable : editable, html_title : true});
	if (editable) {
		kite.browser.dom.eac('div', el_editor_container, 'wu-title-container').appendChild(title_editor.el_editor);
	}
	nbe.dynamic.get_title = title_editor.get_value;

	nbe.dynamic.publish = doc.editors.add('publish_editor', 'publish', {});

	el_editor_container.appendChild(editor.el_editor);

	if (doc.ids.prefix === 'scroller' && doc.ids.write === null) {
		nbe.site.scroller(editor);
	}
};


nbe.site.display_share = function (ids) {
	var share_window, el_share, display_url, section, el_publish_message, el_close, el_email_message;

	share_window = new kite.browser.ui.Window();
	share_window.set_title('Share');

	el_share = kite.browser.dom.ec('div', 'nbe_window share');
	kite.browser.dom.ea('img', el_share).src = '/img/fork.svg';
	kite.browser.dom.ea('h1', el_share).textContent = 'Share';
	kite.browser.dom.ea('p', el_share).textContent = 'Share the write URL with collaborators or share the read or publish URLs with readers.';

	display_url = function (heading, text, url) {
		var el_section, el_heading, el_url;

		el_section = kite.browser.dom.ea('div', el_share);
		el_heading = kite.browser.dom.ea('h2', el_section);
		el_heading.textContent = heading;
		kite.browser.dom.ea('span', el_heading).textContent = text;
		el_url = kite.browser.dom.ea('a', el_section);
		el_url.textContent = url;
		el_url.href = url;
		el_url.target = '_blank';

		return {element : el_section, url : el_url};
	};

	display_url('Write URL', '(Collaborators can edit the document with this URL)', nbe.config.urls(ids).write);
	display_url('Read URL', '(Readers can view the document and see changes as you type)', nbe.config.urls(ids).read);
	section = display_url('Publish URL', '(Readers can view the published version of this document)', nbe.config.urls(ids).publish);

	(function () {
		var el_html;

		el_html = kite.browser.dom.ea('button', section.element);
		el_html.textContent = 'Publish';

		//nbe.dynamic.publish.get_time(); // null or new Date(time)

		el_publish_message = kite.browser.dom.ea('span', section.element);

		el_html.addEventListener('click', function (event) {
			nbe.dynamic.publish.publish(function (response) {

				if (response === 'published') {
					el_publish_message.textContent = 'The document is published!';
					el_publish_message.className = 'message_success';
					section.url.className = 'visible';
				} else if (response === 'not published') {
					el_publish_message.textContent = 'Error, please try again.';
					el_publish_message.className = 'message_failure';
				} else { // null
					el_publish_message.textContent = 'Network error.';
					el_publish_message.className = 'message_failure';
				}
			});
		}, false);
	}());


	(function () {
		var el_section, access, url_handler, el_email, el_write, el_read, el_publish, el_email_address, el_message, el_email_send;

		el_section = kite.browser.dom.ea('div', el_share);

		access = 'publish';

		url_handler = function (e) {
			el_write.className = '';
			el_read.className = '';
			el_publish.className = '';
			if (e.target === el_write) {
				access = 'write';
				el_write.className = 'active';
			} else if (e.target === el_read) {
				access = 'read';
				el_read.className = 'active';
			} else if (e.target === el_publish) {
				access = 'publish';
				el_publish.className = 'active';
			}
		};

		el_email = kite.browser.dom.eac('div', el_section, 'share_email');
		kite.browser.dom.ea('h2', el_email).textContent = 'Share via e-mail';
		kite.browser.dom.ea('div', el_email).textContent = 'Select URL to share:';
		el_write = kite.browser.dom.ea('button', el_email);
		el_write.textContent = 'Write';
		el_write.addEventListener('click', url_handler);
		el_read = kite.browser.dom.ea('button', el_email);
		el_read.textContent = 'Read';
		el_read.addEventListener('click', url_handler);
		el_publish = kite.browser.dom.ea('button', el_email);
		el_publish.textContent = 'Publish';
		el_publish.addEventListener('click', url_handler);
		el_publish.className = 'active';
		kite.browser.dom.ea('div', el_email).textContent = 'E-mail address(es):';
		el_email_address = kite.browser.dom.ea('textarea', el_email);
		el_email_address.setAttribute('autocapitalize', 'none');
		kite.browser.dom.ea('div', el_email).textContent = 'Message (optional):';
		el_message = kite.browser.dom.ea('textarea', el_email);
		el_email_send = kite.browser.dom.eac('button', el_email, 'send');
		el_email_send.textContent = 'Send';
		el_email_send.addEventListener('click', function (e) {
			var body, emails;

			emails = nbe.lib.share_emails(el_email_address.value);

			if (emails.invalid.length === 0 && emails.valid.length !== 0) {
				body = {type : 'share', emails : emails.valid, message : el_message.value, access : access, url : nbe.config.urls(ids)[access], title : nbe.dynamic.get_title()};
				nbe.lib.xhr('POST', nbe.config.share_url, {}, JSON.stringify(body), 0, function (response) {
					el_email_address.value = '';
					el_email_message.textContent = 'The invitation has been sent.';
					el_email_message.className = 'message_success';
				}, function () {}, function () {
					el_email_message.textContent = 'Internet connection error, please try again.';
					el_email_message.className = 'message_failure';
				});
			} else {
				if (emails.invalid.length !== 0) {
					el_email_message.textContent = 'These email addresses are invalid. Please correct them.\n\n' + emails.invalid.join('\n');
				} else {
					el_email_message.textContent = 'Please specify the email address(es).';
				}
				el_email_message.className = 'message_failure';
			}
		}, false);
		el_email_message = kite.browser.dom.ea('span', el_email);
	}());

	el_close = kite.browser.dom.ea('button', el_share);
	el_close.textContent = 'Close';
	el_close.addEventListener('click', function (e) {
		share_window.close();
	}, false);

	share_window.set_content(el_share);

	return {display : function () {
		el_email_message.textContent = '';
		el_publish_message.textContent = '';
		section.element.appendChild(nbe.dynamic.publish.msg);
		if (nbe.dynamic.publish.get_time() === null) {
			section.url.className = 'hidden';
		} else {
			section.url.className = 'visible';
		}
		share_window.open();
	}};
};


nbe.site.display_feedback = function () {
	var el_button, feedback_window, el_feedback, el_name, el_email_address, el_message, el_buttons, el_send, el_send_message, el_close;

	feedback_window = new kite.browser.ui.Window();
	feedback_window.set_title('Feedback');

	el_button = document.getElementById('feedback');
	el_button.addEventListener('click', function (e) {
		feedback_window.open();
	}, false);

	el_feedback = kite.browser.dom.ec('div', 'nbe_window feedback');
	kite.browser.dom.ea('div', el_feedback).innerHTML = '!';
	kite.browser.dom.ea('h1', el_feedback).innerHTML = 'Feedback';
	kite.browser.dom.ea('p', el_feedback).innerHTML = 'Your opinion is very valuable to us, please let us know what you think.';

	kite.browser.dom.ea('h3', el_feedback).innerHTML = 'Name';

	el_name = kite.browser.dom.ea('input', el_feedback);
	el_name.type = 'text';

	kite.browser.dom.ea('h3', el_feedback).innerHTML = 'E-mail';

	el_email_address = kite.browser.dom.input('email', null, null, null, null, null, el_feedback);
	el_email_address.setAttribute('autocapitalize', 'none');

	kite.browser.dom.ea('h3', el_feedback).innerHTML = 'Message';

	el_message = kite.browser.dom.ea('textarea', el_feedback);

	el_buttons = kite.browser.dom.ea('footer', el_feedback);

	el_send = kite.browser.dom.ea('button', el_buttons);
	el_send.innerHTML = 'Send';
	el_send.addEventListener('click', function (e) {
		if (el_message.value) {
			if (!el_email_address.value || (el_email_address.value && nbe.lib.valid_email(el_email_address.value))) {
				var body = {type : 'feedback', name : el_name.value, mail : el_email_address.value, message : el_message.value};
				nbe.lib.xhr('POST', nbe.config.feedback_url, {}, JSON.stringify(body), 0, function (response) {
					el_name.value = '';
					el_email_address.value = '';
					el_message.value = '';
					el_send_message.innerHTML = 'Email sent.';
					el_send_message.className = 'message_success';
					setTimeout(function () {
						kite.browser.animation.Fade_out(el_send_message, {duration : 4000});
					}, 2000);
				}, function () {}, function () {
				 // error
					el_send_message.innerHTML = 'Server error, please try again.';
					el_send_message.className = 'message_failure';
					setTimeout(function () {
						kite.browser.animation.Fade_out(el_send_message, {duration : 4000});
					}, 2000);
				});
			} else {
				el_send_message.innerHTML = 'The email address is incorrect.';
				el_send_message.className = 'message_failure';
				setTimeout(function () {
					kite.browser.animation.Fade_out(el_send_message, {duration : 4000});
				}, 2000);
			}
		} else {
			el_send_message.innerHTML = 'Please write a message.';
			el_send_message.className = 'message_failure';
			setTimeout(function () {
				kite.browser.animation.Fade_out(el_send_message, {duration : 4000});
			}, 2000);
		}
	}, false);

	el_send_message = kite.browser.dom.ea('div', el_buttons);

	el_close = kite.browser.dom.ea('button', el_buttons);
	el_close.innerHTML = 'Close';
	el_close.addEventListener('click', function (e) {
		feedback_window.close();
	}, false);

	feedback_window.set_content(el_feedback);
};


nbe.site.display_export = function () {
	var export_window, el_export, el_section, el_word, el_html, el_close;

	export_window = new kite.browser.ui.Window();
	export_window.set_title('Export');

	el_export = kite.browser.dom.ec('div', 'nbe_window share');
	kite.browser.dom.ea('img', el_export).src = '/img/export.svg';
	kite.browser.dom.ea('h1', el_export).textContent = 'Export';
	kite.browser.dom.ea('p', el_export).textContent = 'Please select format by clicking one of the buttons and the file will be downloaded to your device.';

	el_section = kite.browser.dom.ea('div', el_export);
	kite.browser.dom.ea('p', el_section).textContent = 'Please note that export currently only works in Google Chrome.';

	el_word = kite.browser.dom.ea('button', el_section);
	el_word.textContent = 'Word';
	el_word.addEventListener('click', function (e) {
		nbe.lib.save_as(new Blob([nbe.doc.html(nbe.dynamic.doc)], {type : 'application/vnd.ms-word'}), nbe.dynamic.get_title() + '.doc');
	}, false);

	el_html = kite.browser.dom.ea('button', el_section);
	el_html.textContent = 'HTML';
	el_html.addEventListener('click', function (e) {
		nbe.lib.save_as(new Blob([nbe.doc.html(nbe.dynamic.doc)], {type : 'text/html'}), nbe.dynamic.get_title() + '.html');
	}, false);

	kite.browser.dom.ea('p', el_export);

	el_close = kite.browser.dom.ea('button', el_export);
	el_close.textContent = 'Close';
	el_close.addEventListener('click', function (e) {
		export_window.close();
	}, false);

	export_window.set_content(el_export);

	return {display : function () {
		export_window.open();
	}};
};


nbe.site.doc_noexist = function (doc) {
	var el_message;

	el_message = kite.browser.dom.eac('div', document.body, 'full_screen_message');
	kite.browser.dom.ea('div', el_message).textContent = 'The document is not known to the server.';
};


nbe.site.wrong_password = function () {
	var el_message;

	el_message = kite.browser.dom.eac('div', document.body, 'full_screen_message');
	kite.browser.dom.ea('div', el_message).textContent = 'It seems like you\'re not using a proper URL for this document, please check your link.';
};


nbe.site.loading = function () {
	var el_message, status, on, off;

	el_message = document.createElement('div');
	el_message.className = 'full_screen_message';
	kite.browser.dom.ea('div', el_message).textContent = 'We are trying to connect to the server.';

	status = 'init';

	on = function () {
		setTimeout(function () {
			if (status === 'init') {
				status = 'on';
				document.body.appendChild(el_message);
			}
		}, 200);
	};

	off = function () {
		if (status === 'on') {
			document.body.removeChild(el_message);
		}
		status = 'off';
	};

	return {on : on, off : off};
};


nbe.site.supported_doc = function () {
	var el_message = kite.browser.dom.eac('div', document.body, 'full_screen_message');
	kite.browser.dom.ea('div', el_message).innerHTML = 'Your browser is not supported.';
};


nbe.site.supported_front = function (supported) {
	var el_new_button;

	el_new_button = document.getElementById('new_doc');

	if (supported) {
		el_new_button.addEventListener('click', function (e) {
			window.open(nbe.config.new_url(), '_blank');
		}, false);
	} else {
		el_new_button.innerHTML = 'Your browser is not supported.';
		el_new_button.className = 'unsupported';
	}
};


nbe.site.scroller = function (editor) {
	var el_editor, el_scroll;

	el_editor = editor.el_editor;
	el_scroll = el_editor.parentNode.classList.contains('editor_container') ? el_editor.parentNode : el_editor;

	setInterval(function () {
		el_scroll.scrollTop = el_scroll.scrollHeight;
	}, 200);
};


/*
	el_text, el_title, el_panel : elements for insertion of text, title and panel. If they are null, there is no insertion.
	ids = {id, read, write}, if ids.write is null, the editor is read only, otherwise writeable.
	new_doc : is the document new
	ws_url : the url of the web socket to the server.
	local_storage : boolean designating whether local storage is to be used.
	html_title : whtehr the title should be used as title of the full html document.
	callback : get key value pairs.
*/

nbe.site.embed = function (el_text, el_title, el_panel, ids, new_doc, ws_url, local_storage, html_title, callback) {
	var editable, dom_id_to_el, callback_status, doc;

	editable = !(ids.write === null || ids.write === '');

	dom_id_to_el = function (id) {
		return typeof(id) === 'string' ? document.getElementById(id) : id;
	};

	callback_status = function (key, value) {
		var editor, title_editor;

		callback(key, value);
		if (key === 'doc' && value === 'exist') {
			doc.comm.notify();
			editor = doc.editors.add('editor', 'text', {editable : editable});
			if (el_text) {
				dom_id_to_el(el_text).appendChild(editor.el_editor);
			}
			if (el_title) {
				title_editor = doc.editors.add('title_editor', 'title', {editable : editable, html_title : html_title});
				dom_id_to_el(el_title).appendChild(title_editor.el_editor);
			}
			if (el_panel) {
				nbe.site.panel(dom_id_to_el(el_panel), editor);
			}
		}
	};

	ids.new_doc = new_doc;
	doc = nbe.doc.create(ids, local_storage, ws_url, callback_status);

	if (doc.server_status !== 'unknown') {
		callback_status('doc', 'exist');
	}
};


/*
	Helper function to call embed.
	It is used for read only documents.

	el : an element where title and text is inserted. el can be an id of an element.
	ids : an object with id and the read password.
*/

nbe.site.embed_read = function (el, ids) {
	var ws_url, el_title, el_text;

	el = typeof(el) === 'string' ? document.getElementById(el) : el;

	ws_url = 'ws://www.writeurl.com/operations';

	ids.write = null;

	el_title = document.createElement('div');
	el.appendChild(el_title);
	el_text = document.createElement('div');
	el.appendChild(el_text);

	nbe.site.embed(el_text, el_title, null, ids, false, ws_url, true, false, function () {});
};


/*
	Helper function to call embed.
	It is used for write documents.

	el : an element where panel, title and text is inserted. el can be an id of an element.
	ids : an object with id, the read password, and write password.
*/

nbe.site.embed_write = function (el, ids) {
	var ws_url, el_panel, el_title, el_text;

	el = typeof(el) === 'string' ? document.getElementById(el) : el;

	ws_url = 'ws://www.writeurl.com/operations';

	el_panel = document.createElement('div');
	el.appendChild(el_panel);
	el_title = document.createElement('div');
	el.appendChild(el_title);
	el_text = document.createElement('div');
	el.appendChild(el_text);

	console.log(ids);
	nbe.site.embed(el_text, el_title, el_panel, ids, false, ws_url, true, false, function () {});
};


/*
	Helper function to call embed.
	It is used for write documents.

	el : an element where panel, title and text is inserted. el can be an id of an element.
	ids : an object with id, the read password, and write password.
*/

nbe.site.embed_new = function (el) {
	var ws_url, el_panel, el_title, el_text, ids;

	el = typeof(el) === 'string' ? document.getElementById(el) : el;

	ws_url = 'ws://www.writeurl.com/operations';

	el_panel = document.createElement('div');
	el.appendChild(el_panel);
	el_title = document.createElement('div');
	el.appendChild(el_title);
	el_text = document.createElement('div');
	el.appendChild(el_text);

	ids = {
		id : nbe.lib.rnd_string(20),
		read : nbe.lib.rnd_string(20),
		write : nbe.lib.rnd_string(20)
	};

	nbe.site.embed(el_text, el_title, el_panel, ids, true, ws_url, true, false, function () {});

	return ids;
};


// urls:  /text/id/read/write/new

nbe.config = (function () {
	var host, protocol, ws_protocol, home_pathname, valid_id, parse_pathname, publish_pathname, read_pathname,  write_pathname, urls, new_url;

	host = window.location.host;
	protocol = window.location.protocol;
	ws_protocol = protocol == 'http:' ? 'ws:' : 'wss:';

	home_pathname = '/';

	valid_id = function (id) {
		var pattern;

		pattern = /^[a-z0-9]{3,}$/;

		return pattern.test(id);
	};

	parse_pathname = function (pathname) {
		var parts, ids;

		parts = pathname.split('/');
		ids = {
			prefix : parts.length > 1 ? parts[1] : null,
			id : parts.length > 2 && valid_id(parts[2]) ? parts[2] : null,
			read : parts.length > 3 && valid_id(parts[3]) ? parts[3] : null,
			write : parts.length > 4 && valid_id(parts[4]) ? parts[4] : null,
			new_doc : parts.length > 5 && parts[5] === 'new'
		};

		return ids;
	};

	publish_pathname = function (ids) {
		return '/publish/' + ids.id;
	};

	read_pathname = function (ids) {
		return '/text/' + ids.id + '/' + ids.read;
	};

	write_pathname = function (ids) {
		return read_pathname(ids) + '/' + ids.write;
	};

	urls = function (ids) {
		var domain;

		domain = protocol + '//' + host;

		return {
			publish : domain + publish_pathname(ids),
			read : domain + read_pathname(ids),
			write : domain + write_pathname(ids)
		};
	};

	new_url = function () {
		var ids;

		ids = {
			id : nbe.lib.rnd_string(20),
			read : nbe.lib.rnd_string(20),
			write : nbe.lib.rnd_string(20)
		};

		return urls(ids).write + '/new';
	};

	return {
		title : 'My Title',
		home_pathname : home_pathname,
		write_pathname : write_pathname,
		urls : urls,
		new_url : new_url,
		parse_pathname : parse_pathname,
		local_storage : true,
		ws_url : ws_protocol + '//' + host + '/operations',
		share_url : protocol + '//' + host + '/xhr/share',
		feedback_url : protocol + '//' + host + '/xhr/feedback',
		publish_url : protocol + '//' + host + '/xhr/publish',
		file_upload_url : protocol + '//' + host + ':8051'
	};
}());


nbe.lib.clone = function (val) {
	return JSON.parse(JSON.stringify(val));
};


nbe.lib.xhr = function (method, url, headers, body, timeout, callback_200, callback_other, callback_error) {
	var request, prop;

	request = new XMLHttpRequest();

	request.onreadystatechange = function () {
		if (request.readyState === 4) {
			if (request.status === 200) {
				callback_200(request.responseText);
			} else {
				callback_other();
			}
		}
	};

	request.onerror = function () {
		callback_error();
	};

	request.ontimeout = function () {
		callback_error();
	};

	request.open(method, url, true);
	request.timeout = timeout;

	for (prop in headers) {
		if (headers.hasOwnProperty(prop)) {
			request.setRequestHeader(prop, headers[prop]);
		}
	}

	request.send(body);
};


nbe.lib.rnd_random_org = (function () {
	var sent, min, chars, fetch, get;

	sent = false;
	sent = true; // This line is used to block the requests while testing.
	min = 40;

	chars = '';

	fetch = function () {
		var url;

		if (!sent) {
			sent = true;
			url = 'http://www.random.org/strings/?num=3&len=20&digits=on&upperalpha=off&loweralpha=on&unique=off&format=plain&rnd=new';

			nbe.lib.xhr('GET', url, {}, '', 0, function (resp) {
				sent = false;
				try {
					chars = chars + resp.split('\n').join('');
				} catch (e) {}
			}, function () {
				sent = false;
			}, function () {
				sent = false;
			});
		}
	};

	fetch();

	get = function (n) {
		var str;

		str = '';

		if (chars.length >= n) {
			str = chars.slice(0, n);
			chars = chars.slice(n);
		}

		if (chars.length < min) {
			fetch();
		}

		return str;
	};

	return get;
}());


nbe.lib.rnd_crypto = function (n) {
	var chars, buf, i;

	chars = [];

	if ('crypto' in window && 'getRandomValues' in window.crypto) {
		buf = new Uint8Array(n);
		window.crypto.getRandomValues(buf);
		for (i = 0; i < n; i++) {
			chars[i] = buf[i].toString(36).slice(-1);
		}
	}

	return chars.join('');
};


nbe.lib.rnd_math_random = function (n) {
	var chars, i;

	chars = [];

	for (i = 0; i < n; i++) {
		chars[i] = Math.floor(36 * Math.random()).toString(36);
	}

	return chars.join('');
};


nbe.lib.rnd_string = function (n) {
	var str;

	str = nbe.lib.rnd_random_org(n);

	if (str.length !== n) {
		str = nbe.lib.rnd_crypto(n);
	}

	if (str.length !== n) {
		str = nbe.lib.rnd_math_random(n);
	}

	return str;
};


nbe.lib.partial_copy = function (src, dst, keys) {
	var i, key;

	for (i = 0; i < keys.length; i++) {
		key = keys[i];
		if (key in src) {
			dst[key] = src[key];
		}
	}

	return dst;
};


nbe.lib.get_attributes = function (element, keys) {
	var format, set_value, i;

	format = {};

	set_value = function (key) {
		var value;

		value = element.getAttribute('data-' + key);
		if (value) {
			format[key] = value;
		}
	};

	for (i = 0; i < keys.length; i++) {
		set_value(keys[i]);
	}

	return format;
};


nbe.lib.set_attributes = function (element, keys, format) {
	var set_attribute, i;

	set_attribute = function (key) {
		if (key in format) {
			element.setAttribute('data-' + key, format[key]);
		} else {
			element.removeAttribute('data-' + key);
		}
	};

	for (i = 0; i < keys.length; i++) {
		set_attribute(keys[i]);
	}

	return element;
};


nbe.lib.new_id = function () {
	var stem, counter;

	stem = nbe.lib.rnd_string(12);
	counter = 0;

	return function () {
		var id;

		id = stem + counter;
		counter++;

		return id;
	};
};


nbe.lib.valid_email = function (email) {
	var pattern;

	pattern = /^[\-a-z0-9~!$%\^&*_=+}{\'?]+(\.[\-a-z0-9~!$%\^&*_=+}{\'?]+)*@([a-z0-9_][\-a-z0-9_]*(\.[\-a-z0-9_]+)*\.(aero|arpa|biz|com|coop|edu|gov|info|int|mil|museum|name|net|org|pro|travel|mobi|[a-z][a-z])|([0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}))(:[0-9]{1,5})?$/i;

	return typeof email === 'string' && pattern.test(email);
};


nbe.lib.share_emails = function (text) {
	var emails, valid, invalid;

	emails = text.split(/[ ,\n]/).filter(function (email) {
		return email !== '';
	});

	valid = [];
	invalid = [];

	emails.forEach(function (email) {
		if (nbe.lib.valid_email(email)) {
			valid.push(email);
		} else {
			invalid.push(email);
		}
	});

	return {valid : valid, invalid : invalid};
};


nbe.lib.file_upload = function (file, callback) {
	var find_ending, ending, reader;

	find_ending = function (file) {
		var match;

		match = file.name.match(/\.([a-zA-Z]+)/);
		ending = match ? match[1] : null;

		return ending;
	};

	ending = find_ending(file);

	if (ending === null) {
		callback(null);
	} else {
		reader = new FileReader();

		reader.onload = function (event) {
			nbe.lib.xhr('POST', nbe.config.file_upload_url, {'X-File-Ending' : ending}, reader.result, 0, function (responseText) {
				callback(JSON.parse(responseText));
			}, function () {
				callback(null);
			}, function () {
				callback(null);
			});
		};

		reader.readAsArrayBuffer(file);
	}
};


nbe.lib.save_as = (function (view) {
	"use strict";
	var
		doc = view.document,
		get_URL = function () {
			return view.URL || view.webkitURL || view;
		},
		URL = view.URL || view.webkitURL || view,
		save_link = doc.createElementNS("http://www.w3.org/1999/xhtml", "a"),
		can_use_save_link = "download" in save_link,
		click = function (node) {
			var event = doc.createEvent("MouseEvents");
			event.initMouseEvent("click", true, false, view, 0, 0, 0, 0, 0, false, false, false, false, 0, null);
			return node.dispatchEvent(event); // false if event was cancelled
		},
		webkit_req_fs = view.webkitRequestFileSystem,
		req_fs = view.requestFileSystem || webkit_req_fs || view.mozRequestFileSystem,
		throw_outside = function (ex) {
			(view.setImmediate || view.setTimeout)(function () {
				throw ex;
			}, 0);
		},
		force_saveable_type = "application/octet-stream",
		fs_min_size = 0,
		deletion_queue = [],
		process_deletion_queue = function () {
			var i, file;
			i = deletion_queue.length;
			while (i) {
				i = i - 1;
				file = deletion_queue[i];
				if (typeof file === "string") { // file is an object URL
					URL.revokeObjectURL(file);
				} else { // file is a File
					file.remove();
				}
			}
			deletion_queue.length = 0; // clear queue
		},
		dispatch = function (filesaver, event_types, event) {
			event_types = [].concat(event_types);
			var i, listener;
			i = event_types.length;
			while (i) {
				i = i - 1;
				listener = filesaver["on" + event_types[i]];
				if (typeof listener === "function") {
					try {
						listener.call(filesaver, event || filesaver);
					} catch (ex) {
						throw_outside(ex);
					}
				}
			}
		},
		FileSaver = function (blob, name) {
			// First try a.download, then web filesystem, then object URLs
			var
				filesaver = this,
				type = blob.type,
				blob_changed = false,
				object_url,
				target_view,
				get_object_url = function () {
					var object_url = get_URL().createObjectURL(blob);
					deletion_queue.push(object_url);
					return object_url;
				},
				dispatch_all = function () {
					dispatch(filesaver, "writestart progress write writeend".split(" "));
				},
				// on any filesys errors revert to saving with object URLs,
				fs_error = function () {
					// don't create more object URLs than needed
					if (blob_changed || !object_url) {
						object_url = get_object_url(blob);
					}
					target_view.location.href = object_url;
					filesaver.readyState = filesaver.DONE;
					dispatch_all();
				},
				abortable = function (func) {
					return function () {
						if (filesaver.readyState !== filesaver.DONE) {
							return func.apply(this, arguments);
						}
					};
				},
				create_if_not_found = {create: true, exclusive: false},
				slice
			;
			filesaver.readyState = filesaver.INIT;
			if (!name) {
				name = "download";
			}
			if (can_use_save_link) {
				object_url = get_object_url(blob);
				save_link.href = object_url;
				save_link.download = name;
				if (click(save_link)) {
					filesaver.readyState = filesaver.DONE;
					dispatch_all();
					return;
				}
			}
			// Object and web filesystem URLs have a problem saving in Google Chrome when
			// viewed in a tab, so I force save with application/octet-stream
			// http://code.google.com/p/chromium/issues/detail?id=91158
			if (view.chrome && type && type !== force_saveable_type) {
				slice = blob.slice || blob.webkitSlice;
				blob = slice.call(blob, 0, blob.size, force_saveable_type);
				blob_changed = true;
			}
			// Since I can't be sure that the guessed media type will trigger a download
			// in WebKit, I append .download to the filename.
			// https://bugs.webkit.org/show_bug.cgi?id=65440
			if (webkit_req_fs && name !== "download") {
				name += ".download";
			}
			if (type === force_saveable_type || webkit_req_fs) {
				target_view = view;
			} else {
				target_view = view.open();
			}
			if (!req_fs) {
				fs_error();
				return;
			}
			fs_min_size += blob.size;
			req_fs(view.TEMPORARY, fs_min_size, abortable(function (fs) {
				fs.root.getDirectory("saved", create_if_not_found, abortable(function (dir) {
					var save = function () {
						dir.getFile(name, create_if_not_found, abortable(function (file) {
							file.createWriter(abortable(function (writer) {
								writer.onwriteend = function (event) {
									target_view.location.href = file.toURL();
									deletion_queue.push(file);
									filesaver.readyState = filesaver.DONE;
									dispatch(filesaver, "writeend", event);
								};
								writer.onerror = function () {
									var error = writer.error;
									if (error.code !== error.ABORT_ERR) {
										fs_error();
									}
								};
								"writestart progress write abort".split(" ").forEach(function (event) {
									writer["on" + event] = filesaver["on" + event];
								});
								writer.write(blob);
								filesaver.abort = function () {
									writer.abort();
									filesaver.readyState = filesaver.DONE;
								};
								filesaver.readyState = filesaver.WRITING;
							}), fs_error);
						}), fs_error);
					};
					dir.getFile(name, {create: false}, abortable(function (file) {
						// delete file if it already exists
						file.remove();
						save();
					}), abortable(function (ex) {
						if (ex.code === ex.NOT_FOUND_ERR) {
							save();
						} else {
							fs_error();
						}
					}));
				}), fs_error);
			}), fs_error);
		},
		FS_proto = FileSaver.prototype,
		saveAs = function (blob, name) {
			return new FileSaver(blob, name);
		}
	;
	FS_proto.abort = function () {
		var filesaver = this;
		filesaver.readyState = filesaver.DONE;
		dispatch(filesaver, "abort");
	};
	FS_proto.readyState = FS_proto.INIT = 0;
	FS_proto.WRITING = 1;
	FS_proto.DONE = 2;

	FS_proto.error =
	FS_proto.onwritestart =
	FS_proto.onprogress =
	FS_proto.onwrite =
	FS_proto.onabort =
	FS_proto.onerror =
	FS_proto.onwriteend =
		null;

	view.addEventListener("unload", process_deletion_queue, false);
	return saveAs;
}(window.self));

nbe.doc.create = function (ids, use_local_storage, server_url, callback_status) {
	var doc;

	doc = {};
	doc.ids = ids;
	doc.server_status = 'unknown';
	doc.state = nbe.doc.state_init();
	doc.n_operations_server = 0;
	doc.operations_local = [];
	doc.local_storage = nbe.doc.local_storage(doc, use_local_storage);
	doc.local_storage.read();

	if (doc.server_status === 'unknown' && ids.new_doc) {
		doc.server_status = 'new';
		doc.local_storage.write();
	}
	delete ids.new_doc;

	doc.editors = nbe.doc.editors(doc);

	doc.new_id = nbe.lib.new_id();

	doc.add_ops = function (editor_id, ops) {
		var operation;

		operation = {id : doc.new_id(), ops : ops};
		doc.editors.notify(ops, editor_id, true);
		doc.operations_local.push(operation);
		doc.comm.notify();
		doc.local_storage.write();
	};

	doc.comm = nbe.doc.comm(doc, server_url, callback_status);

	callback_status('nunsaved', doc.operations_local.length);

	return doc;
};


nbe.doc.editors = function (doc) {
	var editors, add, remove, notify;

	editors = {};

	add = function (editor_id, editor_type, options) {
		var ops_editor, ops, state, editor, i, j, op;

		ops_editor = [];
		for (i = 0; i < doc.operations_local.length; i++) {
			ops = doc.operations_local[i].ops;
			for (j = 0; j < ops.length; j++) {
				op = ops[j];
				if (editor_type === op.editor_class || (editor_type === 'text' && !('editor_class' in op))) {
					ops_editor.push(op);
				}
			}
		}

		if (editor_type === 'text') {
			state = nbe.state.state_copy(doc.state.text);
			nbe.state.update(null, state, null, ops_editor);
			editor = nbe.editor.create(editor_id, options, doc);
			editor.init(state);
		} else if (editor_type === 'title') {
			state = nbe.title.state_copy(doc.state.title);
			editor = nbe.title.create(editor_id, options, doc);
			editor.init(state);
			editor.add_external_ops(ops_editor, false);
		} else if (editor_type === 'publish') {
			state = nbe.publish.state_copy(doc.state.publish);
			editor = nbe.publish.create(editor_id, doc);
			editor.init(state);
			editor.add_external_ops(ops_editor, false);
		}

		editors[editor_id] = editor;

		return editor;
	};

	remove = function (editor_id) {
		delete editors[editor_id];
	};

	notify = function (ops, excl_editor_id, set_location) {
		var editor_id;

		for (editor_id in editors) {
			if (editors.hasOwnProperty(editor_id) && (excl_editor_id === null || excl_editor_id !== editor_id)) {
				editors[editor_id].add_external_ops(ops, set_location);
			}
		}
	};

	return {add : add, remove : remove, notify : notify};
};


nbe.doc.local_storage = function (doc, use_local_storage) {
	var stringify, parse, timeout, key, read, write, timer, save;

	timeout = 5000;

	stringify = function () {
		return JSON.stringify({
			state : nbe.doc.state_serialize(doc.state),
			server_status : doc.server_status,
			n_operations_server : doc.n_operations_server,
			operations_local : doc.operations_local
		});
	};

	parse = function (value) {
		var parsed;

		parsed = JSON.parse(value);

		doc.state = nbe.doc.state_deserialize(parsed.state);
		doc.server_status = parsed.server_status;
		doc.n_operations_server = parsed.n_operations_server;
		doc.operations_local = parsed.operations_local;
	};

	key = function () {
		return '/nbe/text/' + doc.ids.id;
	};

	read = function () {
		var value;

		value = localStorage.getItem(key());
		if (value) {
			parse(value);
		}
	};

	save = function () {
		localStorage.setItem(key(), stringify());
	};

	timer = null;

	write = function () {
		if (timer === null) {
			timer = setTimeout(function () {
				save();
				timer = null;
			}, timeout);
		}
	};

	if (use_local_storage && typeof(localStorage) === 'object') {
		return {read: read, write : write};
	} else {
		return {read : function () {}, write : function () {}};
	}
};


nbe.doc.merge = function (doc, operations, noperations) {
	var ncommon, operations_server_new, operation_ids, operations_local_new, ops;

	operations = operations.slice(doc.n_operations_server - noperations);

	if (operations.length !== 0) {

		doc.n_operations_server = doc.n_operations_server + operations.length;
		nbe.doc.state_update(doc.state, operations);

		for (ncommon = 0; ncommon < doc.operations_local.length && ncommon < operations.length; ncommon++) {
			if (operations[ncommon].id !== doc.operations_local[ncommon].id) {
				break;
			}
		}

		doc.operations_local = doc.operations_local.slice(ncommon);
		operations_server_new = operations.slice(ncommon);

		if (operations_server_new.length !== 0) {

			operation_ids = {};
			operations_server_new.forEach(function (operation) {
				operation_ids[operation.id] = true;
			});

			operations_local_new = doc.operations_local.filter(function (operation) {
				return !(operation.id in operation_ids);
			});

			ops = [];
			doc.operations_local.forEach(function (operation) {
				ops = ops.concat(operation.ops);
			});
			ops = nbe.state.invert_ops(ops);

			operations_server_new.concat(operations_local_new).forEach(function (operation) {
				ops = ops.concat(operation.ops);
			});

			doc.editors.notify(ops, null, true);
		}
	}
};


nbe.doc.html = function (doc) {
	var title_editor, text_editor, title, text, html;

	title_editor = doc.editors.add('temp', 'title', {editable : false, html_title : false});
	title = title_editor.get_value();
	doc.editors.remove('temp');

	text_editor = doc.editors.add('temp', 'text', {editable : false});
	text = text_editor.get_html();
	doc.editors.remove('temp');

	text = text.replace(/ data-id="[a-z0-9]+"/g, '');
	text = text.replace(/ style=""/g, '');

	html = [
		'<!DOCTYPE html>',
		'<html lang="en">',
		'<head>',
		'<meta http-equiv="Content-type" content="text/html; charset=UTF-8" />',
		'<title>',
		title,
		'</title>',
		'<style type="text/css">',
		nbe.css.publish,
		'</style>',
		'</head>',
		'<body>',
		'<div class="nbe editor">',
		text,
		'</div>',
		'</body>',
		'</html>'
	].join('\n');

	return html;
};


nbe.doc.comm = function (doc, server_url, callback_status) {
	var send_new, receive_new, send_unknown, receive_unknown, send_sync, receive_sync, receive, ws, notify;

	send_new = function () {
		ws.send(JSON.stringify({type : 'new', ids : doc.ids}));
	};

	receive_new = function (msg) {
		if (msg.text === 'created') {
			doc.server_status = 'established';
			doc.local_storage.write();
			send_sync();
		} else {
			console.log('The id is already taken');
		}
	};

	send_unknown = function () {
		ws.send(JSON.stringify({type : 'unknown', ids : doc.ids}));
	};

	receive_unknown = function (msg) {
		if (msg.text === 'noexist') {
			ws.close();
			callback_status('doc', 'noexist');
		} else {
			doc.state =  nbe.doc.state_deserialize(msg.state);
			doc.n_operations_server = msg.noperation;
			doc.server_status = 'established';
			doc.local_storage.write();
			callback_status('doc', 'exist');
		}
	};

	send_sync = function () {
		ws.send(JSON.stringify({type : 'sync', ids : doc.ids, noperations : doc.n_operations_server, operations : doc.operations_local}));
		callback_status('nunsaved', doc.operations_local.length);
	};

	receive_sync = function (msg) {
		var n_operations_pre;

		n_operations_pre = doc.n_operations_server;
		nbe.doc.merge(doc, msg.operations, msg.noperations);
		if (n_operations_pre !== doc.n_operations_server) {
			send_sync();
		}
	};

	receive = function (data) {
		var msg;

		msg = JSON.parse(data);
		switch (msg.type) {
		case 'new':
			receive_new(msg);
			break;
		case 'unknown':
			receive_unknown(msg);
			break;
		case 'invalid':
			ws.close();
			callback_status('password', 'wrong password');
			break;
		case 'sync':
			receive_sync(msg);
			break;
		}
	};

	callback_status('network', 'unconnected');

	if (server_url) {
		ws = nbe.doc.ws(server_url, receive, callback_status);
		if (ws !== null) {
			switch (doc.server_status) {
			case 'new':
				send_new();
				break;
			case 'unknown':
				send_unknown();
				break;
			case 'established':
				send_sync();
				break;
			}
		}
	}

	notify = function () {
		if (server_url && ws !== null && doc.server_status === 'established') {
			send_sync();
		}
	};

	return {notify : notify};
};


nbe.doc.ws = function (url, callback_msg, callback_status) {
	var closed, msg1, msg2, msg_status, send, close, connect, conn;

	if (typeof(WebSocket) === 'undefined' && typeof(MozWebSocket) !== 'function') {
		return null;
	}

	closed = false;
	msg1 = null;
	msg2 = null;
	msg_status = 'received';

	send = function (msg) {
		msg2 = msg;
		if (msg_status === 'received' && conn.readyState === conn.OPEN) {
			msg1 = msg;
			msg_status = 'pending';
			conn.send(msg);
		}
	};

	close = function () {
		closed = true;
		if (conn.readyState !== conn.CLOSED) {
			conn.close();
		}
	};

	connect = function () {
		console.log('connect, url = ', url);

		conn = typeof(WebSocket) !== 'undefined' ?  new WebSocket(url) : new MozWebSocket(url);
		//console.log('connect', new Date(), conn);

		conn.onopen = function () {
			callback_status('network', 'connected');
			//console.log('open', new Date(), conn);
			if (msg2 !== null) {
				send(msg2);
			}
		};

		conn.onerror = function () {
			//console.log('error', new Date(), conn);
			conn.close();
		};

		conn.onclose = function () {
			//console.log('close', new Date(), conn);
			msg_status = 'received';
			callback_status('network', 'unconnected');
			if (!closed) {
				setTimeout(connect, 5000);
			}
		};

		conn.onmessage = function (e) {
			msg_status = 'received';
			callback_msg(e.data);
			if (msg1 !== msg2) {
				send(msg2);
			}
		};
	};

	connect();

	return {send : send, close : close};
};


nbe.doc.state_init = function () {
	return {
		text : nbe.state.deserialize(nbe.state.initial()),
		title : nbe.title.state_init(),
		publish : nbe.publish.state_init()
	};
};


nbe.doc.state_copy = function (state) {
	return {
		text : nbe.state.deserialize(nbe.state.serialize(state.text)),
		title : nbe.title.state_copy(state.title),
		publish : nbe.publish.state_copy(state.publish)
	};
};


nbe.doc.state_update = function (state, operations) {
	var ops;

	ops = {
		text : [],
		title : [],
		publish : []
	};

	operations.forEach(function (operation) {
		operation.ops.forEach(function (op) {
			var editor_class;

			editor_class = 'editor_class' in op ? op.editor_class : 'text';
			ops[editor_class].push(op);
		});
	});

	nbe.state.update(null, state.text, null, ops.text);
	nbe.title.state_update(state.title, ops.title);
	nbe.publish.state_update(state.publish, ops.publish);
};


nbe.doc.state_serialize = function (state) {
	return JSON.stringify({
		text : nbe.state.serialize(state.text),
		title : state.title,
		publish : state.publish
	});
};


nbe.doc.state_deserialize = function (value) {
	var parsed;

	parsed = JSON.parse(value);

	return {
		text : nbe.state.deserialize(parsed.text),
		title : parsed.title,
		publish : parsed.publish
	};
};


nbe.state.initial = function () {
	return JSON.stringify({
		nodes : {
			root : {
				type : 'root',
				id : 'root',
				parent : null,
				children : ['line'],
				val : {}
			},
			line : {
				type : 'line',
				id : 'line',
				parent : 'root',
				children : [],
				val : {}
			}
		}
	});
};


nbe.state.init = function (editor, state) {
	var dom, insert_child_nodes;

	editor.state = state;
	editor.dom = dom = {};

	dom.root = nbe.state.element('root', 'root', state.nodes.root.val);

	insert_child_nodes = function (par, type, nodes) {
		var i, node;

		for (i = 0; i < nodes.length; i++) {
			node = nodes[i];
			dom[node.id] = nbe.state.element(node.id, node.type, node.val);
			if (type === 'line') {
				par.insertBefore(dom[node.id], par.lastChild);
			} else {
				par.appendChild(dom[node.id]);
			}
			insert_child_nodes(dom[node.id], node.type, node.children);
		}
	};

	insert_child_nodes(dom.root, 'root', state.nodes.root.children);

	nbe.state.reset_counter(editor);

	editor.mutation.disconnect();

	while (editor.el_editor.firstChild) {
		editor.el_editor.removeChild(editor.el_editor.firstChild);
	}
	editor.el_editor.appendChild(dom.root);

	editor.mutation.observe();

	return editor;
};


nbe.state.clean = function (editor) {
	nbe.state.init(editor, editor.state);
	nbe.location.set(editor, editor.location);
};


nbe.state.update = function (editor, state, dom, ops) {
	var nodes, root, insert, append, remove, mutate, split, merge, opi, op;

	nodes = state.nodes;
	root = nodes.root;

	insert = function (id, before, type, val) {
		var node, index;

		if (!(id in nodes) && before in nodes) {
			node = {id : id, type : type, val : val, parent : nodes[before].parent, children : []};
			nodes[id] = node;
			index = node.parent.children.indexOf(nodes[before]);
			node.parent.children = node.parent.children.slice(0, index).concat([node]).concat(node.parent.children.slice(index));
			if (dom) {
				dom[id] = nbe.state.element(id, type, val);
				dom[nodes[before].parent.id].insertBefore(dom[id], dom[before]);
			}
		}
	};

	append = function (id, parent_id, type, val) {
		var node;

		if (!(id in nodes) && parent_id in nodes) {
			node = {id : id, type : type, val : val, parent : nodes[parent_id], children : []};
			nodes[id] = node;
			node.parent.children.push(node);
			if (dom) {
				dom[id] = nbe.state.element(id, type, val);
			}
			if (node.parent.type === 'line') {
				if (dom) {
					dom[parent_id].insertBefore(dom[id], dom[parent_id].lastChild);
				}
				nbe.state.line_font_size(state, dom, parent_id, 'append');
			} else {
				if (dom) {
					dom[parent_id].appendChild(dom[id]);
				}
			}
		}
	};

	remove = function (id) {
		var node, index;

		if (id in nodes) {
			node = nodes[id];
			if (node.children.length === 0) {
				if (node.parent.type === 'line') {
					nbe.state.line_font_size(state, dom, node.parent.id, 'remove');
				}
				delete nodes[id];
				index = node.parent.children.indexOf(node);
				node.parent.children = node.parent.children.slice(0, index).concat(node.parent.children.slice(index + 1));
				if (dom) {
					dom[node.parent.id].removeChild(dom[id]);
					delete dom[id];
				}
			}
		}
	};

	mutate = function (id, val) {
		if (id in nodes) {
			nodes[id].val = val;
			if (dom) {
				nbe.state.mutate_element(dom[id], nodes[id].type, val);
			}
		}
	};

	split = function (parent_id, child_id, point_id, parentval, childval) {
		var par, child, index_par, index_point, i, par_child;

		par = nodes[parent_id];
		if (!(child_id in nodes) && par && par.type === 'line') {
			child = {id : child_id, type : 'line', val : childval, parent : root, children : []};
			nodes[child_id] = child;
			if (dom) {
				dom[child_id] = nbe.state.element(child_id, 'line', child.val);
			}
			index_par = root.children.indexOf(par);
			if (index_par === root.children.length - 1) {
				if (dom) {
					dom.root.appendChild(dom[child_id]);
				}
			} else {
				if (dom) {
					dom.root.insertBefore(dom[child_id], dom[root.children[index_par + 1].id]);
				}
			}
			root.children = root.children.slice(0, index_par + 1).concat([child]).concat(root.children.slice(index_par + 1));
			if (point_id && point_id in nodes && nodes[point_id].parent === par) {
				index_point = par.children.indexOf(nodes[point_id]);
			} else {
				index_point = par.children.length;
			}
			for (i = index_point; i < par.children.length; i++) {
				par_child = par.children[i];
				par_child.parent = child;
				if (dom) {
					dom[parent_id].removeChild(dom[par_child.id]);
					dom[child_id].insertBefore(dom[par_child.id], dom[child_id].lastChild);
				}
			}
			child.children = par.children.slice(index_point);
			par.children = par.children.slice(0, index_point);
			par.val = parentval;
			if (dom) {
				nbe.state.mutate_element(dom[parent_id], 'line', parentval);
			}
		}
	};

	merge = function (parent_id, parentval, childval) {
		var par, index_par, child, i, child_child;

		par = nodes[parent_id];
		if (par && par.type === 'line') {
			index_par = root.children.indexOf(par);
			if (index_par < root.children.length - 1) {
				child = root.children[index_par + 1];
				for (i = 0; i < child.children.length; i++) {
					child_child = child.children[i];
					child_child.parent = par;
					if (dom) {
						dom[child.id].removeChild(dom[child_child.id]);
						dom[parent_id].insertBefore(dom[child_child.id], dom[parent_id].lastChild);
					}
				}
				if (dom) {
					dom.root.removeChild(dom[child.id]);
					delete dom[child.id];
				}
				root.children = root.children.slice(0, index_par + 1).concat(root.children.slice(index_par + 2));
				delete nodes[child.id];
				par.children = par.children.concat(child.children);
				par.val = nbe.state.line_val_merge(parentval, childval);
				if (dom) {
					nbe.state.mutate_element(dom[parent_id], 'line', par.val);
				}
			}
		}
	};

	if (dom) {
		editor.mutation.disconnect();
	}

	for (opi = 0; opi < ops.length; opi++) {
		op = ops[opi];
		if (op.domop === 'insert') {
			insert(op.id, op.before, op.type, op.val);
		} else if (op.domop === 'append') {
			append(op.id, op.parent, op.type, op.val);
		} else if (op.domop === 'remove') {
			remove(op.id);
		} else if (op.domop === 'mutate') {
			mutate(op.id, op.after);
		} else if (op.domop === 'split') {
			split(op.parent, op.child, op.point, op.parentval, op.childval);
		} else if (op.domop === 'merge') {
			merge(op.parent, op.parentval, op.childval);
		}
	}

	if (dom) {
		nbe.state.reset_counter(editor);
		editor.mutation.observe();
	}
};


nbe.state.element = function (id, type, val) {
	var name, el;

	name = {
		root : 'div',
		line : 'div',
		text : 'span',
		img : 'img',
		link : 'a'
	}[type];

	el = document.createElement(name);
	el.setAttribute('data-id', id);
	el.classList.add('wu-' + type);

	if (type === 'line') {
		el.appendChild(document.createElement('br'));
	}

	nbe.state.mutate_element(el, type, val);

	return el;
};


nbe.state.mutate_element = function (element, type, val) {
	var add_classes, remove_classes;

	add_classes = function (keys) {
		var i;

		for (i = 0; i < keys.length; i++) {
			if (keys[i] in val) {
				element.classList.add('wu-' + val[keys[i]]);
			}
		}
	};

	remove_classes = function (classes) {
		var i;

		for (i = 0; i < classes.length; i++) {
			element.classList.remove('wu-' + classes[i]);
		}
	};

	switch (type) {
	case 'root' :
		break;
	case 'line' :
		remove_classes(nbe.state.line_classes);
		add_classes(['heading', 'text_align', 'list', 'line_spacing']);
		element.style.marginLeft = val.left_margin ? (val.left_margin + 'px') : '';
		element.style.fontSize = val.font_size || '';
		break;
	case 'text' :
		element.textContent = val.text;
		element.classList[val.bold ? 'add' : 'remove']('wu-bold');
		element.classList[val.italic ? 'add' : 'remove']('wu-italic');
		element.classList[val.underline ? 'add' : 'remove']('wu-underline');
		element.classList[val.strikethrough ? 'add' : 'remove']('wu-strikethrough');
		element.style.color = val.color || '';
		element.style.backgroundColor = val.background_color || '';
		element.style.fontFamily = val.font_family || '';
		element.style.verticalAlign = val.vertical_align || '';
		element.style.fontSize = val.vertical_align ? (val.font_size ? ((0.8 * (Number(val.font_size.slice(0, val.font_size.length - 2)))) + 'px') : '80%') : (val.font_size || '');
		break;
	case 'img' :
		element.src = val.src || '';
		if ('width' in val) {
			element.width = val.width;
		} else {
			element.removeAttribute('width');
		}
		if ('height' in val) {
			element.height = val.height;
		} else {
			element.removeAttribute('height');
		}
		element.title = val.title || '';
		break;
	case 'link' :
		element.href = val.href;
	}

	return element;
};


nbe.state.formats = {

	text : ['bold', 'italic', 'underline', 'strikethrough', 'color', 'background_color', 'font_family', 'font_size', 'vertical_align'],

	line : ['heading', 'text_align', 'left_margin', 'line_spacing', 'list'],

	default_values : {
		bold : 'off',				// text
		italic : 'off',				// text
		underline : 'off',			// text
		strikethrough : 'off',			// text
		color : 'rgb(0, 0, 0)',			// text
		background_color : 'transparent',	// text
		font_family : 'arial',			// text
		font_size : '16px',			// text
		vertical_align : 'baseline',		// text
		heading : 'none',			// line
		text_align : 'left',			// line
		left_margin : 0,			// line
		line_spacing : 'line_spacing_16',	// line
		list : 'none',				// line
		edit_img : null,			// image button
		edit_link : null			// link button
	},

	left_margin : {
		step : 20,
		max : 500
	},

	font_family : ['arial', 'courier', 'helvetica', 'times', 'verdana']
};


nbe.state.line_font_size = function (state, dom, line_id, domop) {
	var line, el_line, child, font_size;

	line = state.nodes[line_id];
	if (dom) {
		el_line = dom[line_id];
	}

	if (domop === 'remove') {
		if (line.children.length === 1) {
			child = line.children[0];
			if (child.type === 'text') {
				font_size = child.val.font_size;
				if (font_size) {
					line.val.font_size = font_size;
					if (dom) {
						nbe.state.mutate_element(el_line, 'line', line.val);
					}
				}
			}
		}
	} else {
		if (line.val.font_size) {
			delete line.val.font_size;
			if (dom) {
				nbe.state.mutate_element(el_line, 'line', line.val);
			}
		}
	}
};


nbe.state.reset_counter = function (editor) {
	var ordered_types, current_type, lines, i, line, type, reset;

	ordered_types = {
		'disc' : true,
		'lower-alpha' : true,
		'lower-roman' : true,
		'square' : true,
		'upper-alpha' : true,
		'upper-roman' : true,
		'ordered' : true
	};

	current_type = null;
	lines = editor.state.nodes.root.children;
	for (i = 0; i < lines.length; i++) {
		line = lines[i];
		type = line.val.list;
		if (type && type in ordered_types) {
			if (type !== current_type) {
				current_type = type;
				reset = true;
			} else {
				reset = false;
			}
		} else {
			current_type = null;
			reset = false;
		}

		if (reset) {
			editor.dom[line.id].classList.add('wu-reset-counter');
		} else {
			editor.dom[line.id].classList.remove('wu-reset-counter');
		}
	}
};


nbe.state.copy_text_format = function (src, dst) {
	var keys, i, key;

	keys = nbe.state.formats.text;

	for (i = 0; i < keys.length; i++) {
		key = keys[i];
		if (key in src) {
			dst[key] = src[key];
		} else {
			delete dst[key];
		}
	}

	return dst;
};


nbe.state.copy_line_format = function (src, dst) {
	var keys, i, key;

	keys = nbe.state.formats.text.concat(nbe.state.formats.line);

	for (i = 0; i < keys.length; i++) {
		key = keys[i];
		if (key in src) {
			dst[key] = src[key];
		} else {
			delete dst[key];
		}
	}

	return dst;
};


nbe.state.line_val_merge = function (parentval, childval) {
	var val, choose_singleton_else_parent;

	val = {};

	choose_singleton_else_parent = function (key) {
		if (key in parentval) {
			val[key] = parentval[key];
		} else if (key in childval) {
			val[key] = childval[key];
		}
	};

	nbe.state.formats.text.concat(nbe.state.formats.line).forEach(function (key) {
		choose_singleton_else_parent(key);
	});

	if ('left_margin' in parentval) {
		val.left_margin = parentval.left_margin;
	} else {
		delete val.left_margin;
	}

	return val;
};


nbe.state.cmp_value_format = function (type, value, format) {
	if (nbe.state.formats.default_values[type] === value) {
		return !(type in format);
	} else {
		return (type in format) && format[type] === value;
	}
};


nbe.state.cmp_text_format = function (format1, format2) {
	var cmp_type, i;

	cmp_type = function (type) {
		if (type in format1 && type in format2) {
			return format1[type] === format2[type];
		} else if (type in format1) {
			return nbe.state.formats.default_values[type] === format1[type];
		} else if (type in format2) {
			return nbe.state.formats.default_values[type] === format2[type];
		} else {
			return true;
		}
	};

	for (i = 0; i < nbe.state.formats.text.length; i++) {
		if (!cmp_type(nbe.state.formats.text[i])) {
			return false;
		}
	}

	return true;
};


nbe.state.set_format = function (type, value, format) {
	if (nbe.state.formats.default_values[type] === value) {
		delete format[type];
	} else {
		format[type] = value;
	}

	return format;
};


nbe.state.line_classes = [
	'center',
	'right',
	'justify',
	'heading1',
	'heading2',
	'heading3',
	'heading4',
	'heading5',
	'heading6',
	'disc',
	'lower-alpha',
	'lower-roman',
	'square',
	'upper-alpha',
	'upper-roman',
	'ordered',
	'line_spacing_05',
	'line_spacing_06',
	'line_spacing_07',
	'line_spacing_08',
	'line_spacing_09',
	'line_spacing_10',
	'line_spacing_11',
	'line_spacing_12',
	'line_spacing_13',
	'line_spacing_14',
	'line_spacing_15',
	'line_spacing_16',
	'line_spacing_17',
	'line_spacing_18',
	'line_spacing_19',
	'line_spacing_20'
];


nbe.state.invert_ops = function (ops) {
	var invert_op, ops_inv, i;

	invert_op = function (op) {
		var inv;

		if ('editor_class' in op && (op.editor_class === 'title' || op.editor_class === 'publish')) {
			inv = {editor_class : op.editor_class, before : op.after, after : op.before};
		} else if (op.domop === 'insert') {
			inv = {domop : 'remove', id : op.id, before : op.before, type : op.type, val : op.val};
		} else if (op.domop === 'append') {
			inv = {domop : 'remove', id : op.id, parent : op.parent, type : op.type, val : op.val};
		} else if (op.domop === 'remove' && 'before' in op) {
			inv = {domop : 'insert', id : op.id, before : op.before, type : op.type, val : op.val};
		} else if (op.domop === 'remove' && 'parent' in op) {
			inv = {domop : 'append', id : op.id, parent : op.parent, type : op.type, val : op.val};
		} else if (op.domop === 'mutate') {
			inv = {domop : 'mutate', id : op.id, before : op.after, after : op.before};
		} else if (op.domop === 'split' || op.domop === 'merge') {
			inv = {domop : 'merge', parent : op.parent, child : op.child, point : op.point, parentval : op.parentval, childval : op.childval};
			inv.domop = op.domop === 'split' ? 'merge' : 'split';
		}

		return inv;
	};

	ops_inv = [];
	for (i = 0; i < ops.length; i++) {
		ops_inv.push(invert_op(ops[i]));
	}
	ops_inv = ops_inv.reverse();

	return ops_inv;
};


nbe.state.invert_oploc = function (oploc) {
	var oploc_inv;

	oploc_inv = {
		ops : nbe.state.invert_ops(oploc.ops),
		loc_before : oploc.loc_after,
		loc_after : oploc.loc_before
	};

	return oploc_inv;
};


nbe.state.left_margin = function (direction, val) {
	var step, old_value, new_value;

	step = 20;

	old_value = val.left_margin ? val.left_margin : 0;
	if (direction === 'increment') {
		new_value = old_value + step;
	} else {
		new_value = old_value >= step ? old_value - step : old_value;
	}

	if (new_value > 0) {
		val.left_margin = new_value;
	} else {
		delete val.left_margin;
	}

	return new_value !== old_value;
};


nbe.state.serialize = function (state) {
	var new_nodes, nodes, id, node, new_node, i;

	new_nodes = {};
	nodes = state.nodes;
	for (id in nodes) {
		if (nodes.hasOwnProperty(id)) {
			node = nodes[id];
			new_node = {type : node.type, id : node.id, val : node.val, children : []};
			if (node.parent) {
				new_node.parent = node.parent.id;
			}
			for (i = 0; i < node.children.length; i++) {
				new_node.children[i] = node.children[i].id;
			}
			new_nodes[id] = new_node;
		}
	}

	return JSON.stringify({nodes : new_nodes});
};


nbe.state.deserialize = function (str) {
	var new_nodes, nodes, id, node, new_node, i;

	new_nodes = {};
	nodes = JSON.parse(str).nodes;
	for (id in nodes) {
		if (nodes.hasOwnProperty(id)) {
			node = nodes[id];
			new_nodes[id] = {type : node.type, id : node.id, val : node.val, children : []};
		}
	}

	for (id in nodes) {
		if (nodes.hasOwnProperty(id)) {
			node = nodes[id];
			new_node = new_nodes[id];
			if (node.parent) {
				new_node.parent = new_nodes[node.parent];
			}
			for (i = 0; i < node.children.length; i++) {
				new_node.children[i] = new_nodes[node.children[i]];
			}
		}
	}

	return {nodes : new_nodes};
};


nbe.state.state_copy = function (state) {
	return nbe.state.deserialize(nbe.state.serialize(state));
};


nbe.location.get = function (editor) {
	var location, range, find_location, clean;

	location = {};
	range = window.getSelection().getRangeAt(0);

	find_location = function (container, offset) {
		var el;

		if (container.classList) {
			el = container;
		} else {
			el = container.parentNode;
		}

		return {container : el.getAttribute('data-id'), offset : offset};
	};

	clean = function (point) {
		var root, node, offset;

		if (point.container === 'editor') {
			root = editor.state.nodes.root;
			if (point.offset === 0) {
				return {container : root.children[0].id, offset : 0};
			} else {
				node = root;
				while (node.children.length > 0) {
					node = node.children[node.children.length - 1];
				}
				return {container : node.id, offset : (node.type === 'text') ? node.val.text.length : 1};
			}
		}

		if (point.container === 'root') {
			return {container : editor.state.nodes.root.children[point.offset].id, offset : 0};
		}

		if (point.container in editor.state.nodes) {
			node = editor.state.nodes[point.container];
			offset = point.offset;
		}

		if (offset === 0 && node.type === 'line') {
			return point;
		} else if (offset === 0) {
			return nbe.location.loc_previous(node).start;
		} else if (node.type === 'line' || node.type === 'link') {
			return nbe.location.loc_end(node.children[offset - 1]);
		} else {
			return point;
		}
	};

	location.start = clean(find_location(range.startContainer, range.startOffset));
	if (range.collapsed) {
		location.collapsed = true;
	} else {
		location.collapsed = false;
		location.end = clean(find_location(range.endContainer, range.endOffset));
	}

	editor.location = location;

	return location;
};


nbe.location.set = function (editor, location) {
	var find_container_offset, container_offset_start, container_offset_end, range, selection;

	find_container_offset = function (id, offset) {
		var node, new_id, new_offset, container, new_node;

		node = editor.state.nodes[id];
		if (node) {
			if (node.type === 'img') {
				new_id = node.parent.id;
				new_offset = node.parent.children.indexOf(node) + 1;
			} else {
				new_id = id;
				new_offset = offset;
			}

			container = editor.dom[new_id];
			new_node = editor.state.nodes[new_id];

			if (new_node.type === 'text') {
				container = container.firstChild;
				if (new_offset > new_node.val.length) {
					new_offset = new_node.val.length;
				}
			}

			return {container : container, offset : new_offset};
		} else {
			return null;
		}
	};

	editor.mutation.disconnect();

	if (location) {
		container_offset_start = find_container_offset(location.start.container, location.start.offset);
		if (location.collapsed) {
			container_offset_end = container_offset_start;
		} else {
			container_offset_end = find_container_offset(location.end.container, location.end.offset);
		}

		if (container_offset_start && container_offset_end) {
			range = document.createRange();
			range.setStart(container_offset_start.container, container_offset_start.offset);
			range.setEnd(container_offset_end.container, container_offset_end.offset);
			selection = window.getSelection();
			selection.removeAllRanges();
			selection.addRange(range);
		} else {
			location = null;
		}
	}

	editor.location = location;
	if (location) {
		nbe.location.focus(editor);
		nbe.location.scroll(editor);
		editor.inputs.notify();
	} else {
		nbe.location.blur(editor);
	}

	editor.mutation.observe();
};


nbe.location.focus = function (editor) {
	editor.el_editor.focus();

	/*
	cowriter.editor.state.update_state(view);
	cowriter.editor.cursor.scroll_into_view(view);
	cowriter.editor.view.panel_take_over(view);
	*/
};


nbe.location.scroll = function (editor) {
	var el_editor, el_scroll, find_pos, end, element, pos_location, pos_el_scroll, pos, scroll_top;

	el_editor = editor.el_editor;
	el_scroll = el_editor.parentNode.classList.contains('editor_container') ? el_editor.parentNode : el_editor;

	find_pos = function (el) {
		var pos;

		pos = 0;
		while (el) {
			pos = pos + el.offsetTop;
			el = el.offsetParent;
		}

		return pos;
	};

	end = editor.location.collapsed ? editor.location.start : editor.location.end;
	element = editor.dom[end.container];

	pos_location = find_pos(element);
	pos_el_scroll = find_pos(el_scroll);
	pos = pos_location - pos_el_scroll;

	if (el_scroll.scrollTop > pos) {
		el_scroll.scrollTop = pos;
	} else {
		scroll_top = pos + element.offsetHeight - el_scroll.offsetHeight;
		if (el_scroll.scrollTop < scroll_top) {
			el_scroll.scrollTop = scroll_top;
		}
	}
};


nbe.location.blur = function (editor) {
	editor.el_editor.blur();
};


nbe.location.format = function (editor) {
	var format;

	format = {};
	nbe.location.format_line(editor, format);
	nbe.location.format_text(editor, format);

	//nbe.location.format_left_margin(editor, format);
	nbe.location.format_img_link(editor, format);

	editor.format = format;
	editor.inputs.notify();

	return format;
};


nbe.location.format_update = function (editor) {
	nbe.location.format_line(editor, editor.format);
	nbe.location.format_text(editor, editor.format);

	//nbe.location.format_left_margin(editor, editor.format);
	nbe.location.format_img_link(editor, editor.format);

	editor.inputs.notify();

	return editor.format;
};


nbe.location.format_text = function (editor, format) {
	var find_previous_text_or_line, find_next_text_or_line, node_first, node_between, val, point, node_location, node_val, node_previous;

	find_previous_text_or_line = function (node) {
		node = nbe.location.previous_node(node);
		while (node !== null && node.type !== 'text' && node.type !== 'line') {
			node = nbe.location.previous_node(node);
		}

		return node;
	};

	find_next_text_or_line = function (node) {
		node = nbe.location.next_node(node);
		while (node !== null && node.type !== 'text' && node.type !== 'line') {
			node = nbe.location.next_node(node);
		}

		return node;
	};

	node_first = function (node_line) {
		var node_next;

		node_next = find_next_text_or_line(node_line);
		if (node_next && node_next.type === 'text') {
			return node_next;
		} else {
			return node_line;
		}
	};

	node_between = function (node) {
		var node_previous, node_next;

		node_previous = find_previous_text_or_line(node);
		if (node_previous.type === 'text') {
			return node_previous;
		}

		node_next = find_next_text_or_line(node);
		if (node_next && node_next.type === 'text') {
			return node_next;
		}

		return node_previous;
	};

	if (editor.location === null) {
		val = {};
	} else {
		point = editor.location.collapsed ? editor.location.start : editor.location.end;
		node_location = editor.state.nodes[point.container];

		if (node_location.type === 'text' && point.offset > 0) {
			node_val = node_location;
		} else if (node_location.type === 'text') {
			node_previous = nbe.location.previous_node(node_location);
			if (node_previous.type === 'text') {
				node_val = node_previous;
			} else {
				node_val = node_location;
			}
		} else if (node_location.type === 'line') {
			node_val = node_first(node_location);
		} else {
			node_val = node_between(node_location);
		}

		val = node_val.val;
	}

	nbe.state.copy_text_format(val, format);

	return format;
};


nbe.location.format_line = function (editor, format) {
	var find_line_val, line_val, point, node_location;

	find_line_val = function (node) {
		while (node.type !== 'line') {
			node = node.parent;
		}

		return node.val;
	};

	if (editor.location === null) {
		line_val = {};
	} else {
		point = editor.location.collapsed ? editor.location.start : editor.location.end;
		node_location = editor.state.nodes[point.container];
		line_val = find_line_val(node_location);
	}

	nbe.state.copy_line_format(line_val, format);

	return format;
};


nbe.location.format_img_link = function (editor, format) {
	var set_node_img_link, node_start, node_end, offset, node_traverse, cont, node_img, node_link, node_next;

	set_node_img_link = function (node) {
		if (node && node.type === 'img' && node_img === null) {
			node_img = node;
		}

		if (node_link === null) {
			if (node && node.type === 'link') {
				node_link = node;
			} else if (node && node.parent && node.parent.type === 'link') {
				node_link = node.parent;
			}
		}
	};

	if (editor.location === null) {
		return null;
	}

	if (editor.location.collapsed) {
		node_start = node_end = editor.state.nodes[editor.location.start.container];
		offset = editor.location.start.offset;
	} else {
		node_start = editor.state.nodes[editor.location.start.container];
		node_end = editor.state.nodes[editor.location.end.container];
		offset = editor.location.end.offset;
	}

	node_traverse = node_end;
	cont = true;
	node_img = null;
	node_link = null;
	while (cont) {
		set_node_img_link(node_traverse);

		if (node_traverse === node_start) {
			cont = false;
		} else {
			node_traverse = nbe.location.previous_node(node_traverse);
		}
	}

	if (!(node_end.type === 'text' && offset < node_end.val.text.length)) {
		node_next = nbe.location.next_node(node_end);
		set_node_img_link(node_next);
	}

	if (node_img) {
		format.edit_img = {id : node_img.id};
		nbe.lib.partial_copy(node_img.val, format.edit_img, ['src', 'width', 'height', 'title']);
	}

	if (node_link) {
		format.edit_link = {id : node_link.id, href : node_link.val.href};
	}

	return format;
};


nbe.location.get_format = function (editor) {
	nbe.location.get(editor);
	nbe.location.format(editor);
};


nbe.location.previous_node = function (node) {
	var last_descendant, index;

	last_descendant = function (node2) {
		if (node2.children.length === 0) {
			return node2;
		} else {
			return last_descendant(node2.children[node2.children.length - 1]);
		}
	};

	if (node.parent) {
		index = node.parent.children.indexOf(node);
		if (index > 0) {
			return last_descendant(node.parent.children[index - 1]);
		} else {
			return node.parent;
		}
	} else {
		return null;
	}
};


nbe.location.next_node = function (node) {
	var next_sibling_or_higher;

	next_sibling_or_higher = function (node) {
		var index;

		if (node.parent) {
			index = node.parent.children.indexOf(node);
			if (index < node.parent.children.length - 1) {
				return node.parent.children[index + 1];
			} else {
				return next_sibling_or_higher(node.parent);
			}
		} else {
			return null;
		}
	};

	if (node.children.length === 0) {
		return next_sibling_or_higher(node);
	} else {
		return node.children[0];
	}
};


nbe.location.insert_after = function (editor, id) {
	var node, index;

	node = editor.state.nodes[id];
	index = node.parent.children.indexOf(node);
	if (index < node.parent.children.length - 1) {
		return {domop : 'insert', before : node.parent.children[index + 1].id};
	} else {
		return {domop : 'append', parent : node.parent.id};
	}
};


nbe.location.parent_line = function (editor, id) {
	var node;

	node = editor.state.nodes[id];
	while (node && node.type !== 'line') {
		node = node.parent;
	}

	return node;
};


nbe.location.op_remove = function (node) {
	var op, index;

	op = {domop : 'remove', id : node.id, type : node.type, val : node.val};
	index = node.parent.children.indexOf(node);
	if (index === node.parent.children.length - 1) {
		op.parent = node.parent.id;
	} else {
		op.before = node.parent.children[index + 1].id;
	}

	return op;
};


nbe.location.loc_previous = function (node) {
	var node_end, index, node_previous;

	node_end = function (node) {
		if (node.type === 'text') {
			return {container : node.id, offset : node.val.text.length};
		} else if (node.type === 'link') {
			return node_end(node.children[node.children.length - 1]);
		} else if (node.type === 'line') {
			if (node.children.length === 0) {
				return {container : node.id, offset : 0};
			} else {
				return node_end(node.children[node.children.length - 1]);
			}
		} else {
			return {container : node.id, offset : 1};
		}
	};

	index = node.parent.children.indexOf(node);
	if (index > 0) {
		node_previous = node.parent.children[index - 1];
		return {start : node_end(node_previous), collapsed : true};
	} else if (node.type === 'line') {
		return {start : {container : node.id, offset : 0}, collapsed : true};
	} else if (node.parent.type === 'line') {
		return {start : {container : node.parent.id, offset : 0}, collapsed : true};
	} else {
		return nbe.location.loc_previous(node.parent);
	}
};


nbe.location.loc_end = function (node) {
	if (node.type === 'text') {
		return {container : node.id, offset : node.val.text.length};
	} else if (node.type === 'link') {
		return nbe.location.loc_end(node.children[node.children.length - 1]);
	} else if (node.type === 'line') {
		if (node.children.length === 0) {
			return {container : node.id, offset : 0};
		} else {
			return nbe.location.loc_end(node.children[node.children.length - 1]);
		}
	} else {
		return {container : node.id, offset : 1};
	}
};


nbe.location.line = function (node) {
	while (node.type !== 'line') {
		node = node.parent;
	}

	return node;
};


nbe.location.lines = function (editor) {
	var lines, nodes, start, end, node_line_start, node_line_end, children, index_start, index_end;

	lines = [];

	if (editor.location) {
		nodes = editor.state.nodes;
		start = editor.location.start;
		end = editor.location.collapsed ? start : editor.location.end;

		node_line_start = nbe.location.parent_line(editor, start.container);
		node_line_end = nbe.location.parent_line(editor, end.container);

		children = node_line_start.parent.children;

		index_start = children.indexOf(node_line_start);
		index_end = children.indexOf(node_line_end);

		lines = children.slice(index_start, index_end + 1);
	}

	return lines;
};


nbe.location.next_sibling = function (node) {
	var index;

	index = node.parent.children.indexOf(node);
	if (index < node.parent.children.length - 1) {
		return node.parent.children[index + 1];
	} else {
		return null;
	}
};


nbe.location.previous_sibling = function (node) {
	var index;

	index = node.parent.children.indexOf(node);
	if (index > 0) {
		return node.parent.children[index - 1];
	} else {
		return null;
	}
};


nbe.location.in_text = function (point) {
	return point && point.node.type === 'text' && point.offset < point.node.val.text.length && point.offset > 0;
};


nbe.location.in_link = function (point) {
	var index;

	if (point.node.parent.type !== 'link') {
		return false;
	}

	index = point.node.parent.children.indexOf(point.node);
	if (index === point.node.parent.children.length - 1) {
		if (point.node.type === 'text') {
			return nbe.location.in_text(point);
		} else {
			return false;
		}
	} else {
		return true;
	}
};


nbe.location.previous_location = function (editor, loc) {
	var node_end, node, node_prev, node_parent_prev;

	node_end = function (node) {
		if (node.type === 'text') {
			return {container : node.id, offset : node.val.text.length};
		} else if (node.type === 'link') {
			return node_end(node.children[node.children.length - 1]);
		} else if (node.type === 'line') {
			if (node.children.length === 0) {
				return {container : node.id, offset : 0};
			} else {
				return node_end(node.children[node.children.length - 1]);
			}
		} else {
			return {container : node.id, offset : 1};
		}
	};

	node = editor.state.nodes[loc.container];

	if (node.type === 'text' && loc.offset > 1) {
		return {container : node.id, offset : loc.offset - 1};
	} else if (node.type === 'line') {
		node_prev = nbe.location.previous_sibling(node);
		if (node_prev) {
			return node_end(node_prev);
		} else {
			return loc;
		}
	} else if (node.parent.type === 'line') {
		node_prev = nbe.location.previous_sibling(node);
		if (node_prev) {
			return node_end(node_prev);
		} else {
			return {container : node.parent.id, offset : 0};
		}
	} else {
		node_prev = nbe.location.previous_sibling(node);
		if (node_prev) {
			return node_end(node_prev);
		} else {
			node_parent_prev = nbe.location.previous_sibling(node.parent);
			if (node_parent_prev) {
				return node_end(node_parent_prev);
			} else {
				return {container : node.parent.parent.id, offset : 0};
			}
		}
	}
};


nbe.location.first_child = function (node) {
	if (node.children.length === 0) {
		return null;
	} else {
		return node.children[0];
	}
};


nbe.location.last_child = function (node) {
	if (node.children.length === 0) {
		return null;
	} else {
		return node.children[node.children.length - 1];
	}
};


nbe.location.split_merge_point = function (point) {
	var end_of, line_child;

	if (point.node.type === 'line') {
		line_child = nbe.location.first_child(point.node);
		end_of = false;
	} else if (point.node.parent.type === 'link') {
		line_child = point.node.parent;
		end_of = !nbe.location.in_link(point);
	} else {
		line_child = point.node;
		end_of = !nbe.location.in_text(point);
	}

	if (end_of) {
		line_child = nbe.location.next_sibling(line_child);
	}

	return line_child ? line_child.id : null;
};


nbe.location.loc_to_point = function (editor, loc) {
	return {node : editor.state.nodes[loc.container], offset : loc.offset};
};


nbe.location.item_to_loc = function (iditem) {
	var offset, item;

	item = iditem.item;
	offset = item.type === 'text' ? item.val.text.length : 1;

	return {container : iditem.id, offset : offset};
};


nbe.location.text_nodes_in_line = function (line) {
	var nodes, i, node, j;

	nodes = [];
	for (i = 0; i < line.children.length; i++) {
		node = line.children[i];
		if (node.type === 'text') {
			nodes.push(node);
		} else if (node.type === 'link') {
			for (j = 0; j < node.children.length; j++) {
				if (node.children[j].type === 'text') {
					nodes.push(node.children[j]);
				}
			}
		}
	}

	return nodes;
};


nbe.ops.append = function (editor, id, items) {
	var ops, iditem, fill, i, item, new_id;

	ops = [];
	iditem = null;

	fill = function (ops, parent_id, items) {
		var i, new_id, item;

		for (i = 0; i < items.length; i++) {
			new_id = editor.new_id();
			item = items[i];
			ops.push({domop : 'append', id : new_id, parent : parent_id, type : item.type, val : item.val});
			iditem = {id : new_id, item : item};
			fill(ops, new_id, item.children);
		}
	};

	for (i = 0; i < items.length; i++) {
		item = items[i];
		new_id = editor.new_id();
		ops.push({domop : 'append', id : new_id, parent : id, type : item.type, val : item.val});
		iditem = {id : new_id, item : item};
		fill(ops, new_id, item.children);
	}

	return ops.length > 0 ? {ops : ops, loc : nbe.location.item_to_loc(iditem)} : null;
};


nbe.ops.insert_before = function (editor, id, items) {
	var ops, iditem, fill, i, item, new_id;

	ops = [];
	iditem = null;

	fill = function (ops, parent_id, items) {
		var i, new_id, item;

		for (i = 0; i < items.length; i++) {
			new_id = editor.new_id();
			item = items[i];
			ops.push({domop : 'append', id : new_id, parent : parent_id, type : item.type, val : item.val});
			iditem = {id : new_id, item : item};
			fill(ops, new_id, item.children);
		}
	};

	for (i = 0; i < items.length; i++) {
		item = items[i];
		new_id = editor.new_id();
		ops.push({domop : 'insert', id : new_id, before : id, type : item.type, val : item.val});
		iditem = {id : new_id, item : item};
		fill(ops, new_id, item.children);
	}

	return ops.length > 0 ? {ops : ops, loc : nbe.location.item_to_loc(iditem)} : null;
};


nbe.ops.insert_after = function (editor, id, items) {
	var node, next;

	node = editor.state.nodes[id];
	next = nbe.location.next_sibling(node);

	if (next) {
		return nbe.ops.insert_before(editor, next.id, items);
	} else {
		return nbe.ops.append(editor, node.parent, items);
	}
};


nbe.ops.remove = function (node) {
	var before_parent, remove;

	before_parent = function (node, op) {
		var index;

		index = node.parent.children.indexOf(node);
		if (index === node.parent.children.length - 1) {
			op.parent = node.parent.id;
		} else {
			op.before = node.parent.children[index + 1].id;
		}
		return op;
	};

	remove = function (node, ops) {
		var i;

		for (i = 0; i < node.children.length; i++) {
			remove(node.children[i], ops);
		}
		ops.push(before_parent(node, {domop : 'remove', id : node.id, type : node.type, val : node.val}));

		return ops;
	};

	return remove(node, []);
};


nbe.ops.text = function (editor, start, end, insertion) {
	var node, op_mutate, ops, loc, op_start, oploc;

	node = start ? start.node : end.node;

	op_mutate = {domop : 'mutate', id : node.id, before : node.val, after : nbe.lib.clone(node.val)};
	ops = [op_mutate];
	loc = null;

	if (insertion) {
		op_mutate.after.text = node.val.text.slice(end.offset);
		if (start) {
			op_start = {domop : 'insert', id : editor.new_id(), before : node.id, type : 'text', val : nbe.lib.clone(node.val)};
			op_start.val.text = node.val.text.slice(0, start.offset);
			ops.push(op_start);
			loc = {container : op_start.id, offset : start.offset};
		}
		oploc = nbe.ops.insert_before(editor, node.id, insertion);
		if (oploc) {
			ops = ops.concat(oploc.ops);
			if (oploc.loc) {
				loc = oploc.loc;
			}
		}
	} else {
		op_mutate.after.text = (start ?  node.val.text.slice(0, start.offset) : '') + (end ?  node.val.text.slice(end.offset) : '');
		loc = start ? {container : node.id, offset : start.offset} : null;
	}

	return {ops : ops, loc : loc};
};


nbe.ops.link = function (editor, start, end, insertion) {
	var prune, node, link_offset_start, end_of_end, link_offset_end, ops, loc, oploc, i;

	prune = function (ins) {
		var out, i;

		out = [];
		for (i = 0; i < ins.length; i++) {
			if (ins[i].type !== 'link') {
				out.push(ins[i]);
			} else {
				out = out.concat(ins[i].children);
			}
		}

		return out;
	};

	if (insertion) {
		insertion = prune(insertion);
	}

	node = start ? start.node.parent : end.node.parent;

	link_offset_start = start ? node.children.indexOf(start.node) + 1 : 0;

	if (end) {
		end_of_end = !nbe.location.in_text(end);
		link_offset_end = node.children.indexOf(end.node) + (end_of_end ? 1 : 0);
	} else {
		end_of_end = true;
		link_offset_end = node.children.length;
	}

	ops = [];
	loc = null;

	if (link_offset_end < link_offset_start) {
		oploc = nbe.ops.text(editor, start, end, insertion);
		ops = ops.concat(oploc.ops);
		loc = oploc.loc;
	} else {
		if (nbe.location.in_text(start)) {
			oploc = nbe.ops.text(editor, start, null, null);
			ops = ops.concat(oploc.ops);
			loc = oploc.loc;
		} else {
			loc = start ? {container : start.node.id, offset : start.offset} : null;
		}

		for (i = link_offset_start; i < link_offset_end; i++) {
			ops = ops.concat(nbe.ops.remove(node.children[i]));
		}

		if (end_of_end) {
			if (insertion) {
				oploc = nbe.ops.insert_after(editor, end.node.id, insertion);
				if (oploc) {
					ops = ops.concat(oploc.ops);
					if (oploc.loc) {
						loc = oploc.loc;
					}
				}
			}
		} else {
			oploc = nbe.ops.text(editor, null, end, insertion);
			ops = ops.concat(oploc.ops);
			if (oploc.loc) {
				loc = oploc.loc;
			}
		}
	}

	return {ops : ops, loc : loc};
};


nbe.ops.line = function (editor, start, end, insertion) {
	var node, line_offset_start, line_child_start, line_offset_end, line_child_end, ops, loc, oploc, i;

	if (start) {
		if (start.node.type === 'line') {
			node = start.node;
			line_offset_start = 0;
			line_child_start = null;
		} else if (start.node.parent.type === 'line') {
			node = start.node.parent;
			line_offset_start = node.children.indexOf(start.node) + 1;
			line_child_start = nbe.location.in_text(start) ? start.node : null;
		} else if (start.node.parent.type === 'link') {
			node = start.node.parent.parent;
			line_offset_start = node.children.indexOf(start.node.parent) + 1;
			line_child_start = nbe.location.in_link(start) ? start.node.parent : null;
		}
	} else {
		line_offset_start = 0;
		line_child_start = null;
	}

	if (end) {
		if (end.node.type === 'line') {
			node = end.node;
			line_offset_end = 0;
			line_child_end = null;
		} else if (end.node.parent.type === 'line') {
			node = end.node.parent;
			line_offset_end = node.children.indexOf(end.node) + (nbe.location.in_text(end) ? 0 : 1);
			line_child_end = nbe.location.in_text(end) ? end.node : null;
		} else if (end.node.parent.type === 'link') {
			node = end.node.parent.parent;
			line_offset_end = node.children.indexOf(end.node.parent) + (nbe.location.in_link(end) ? 0 : 1);
			line_child_end = nbe.location.in_link(end) ? end.node.parent : null;
		}
	} else {
		line_offset_end = node.children.length;
		line_child_end = null;
	}

	ops = [];
	loc = start ? {container : start.node.id, offset : start.offset} : {container : node.id, offset : 0};

	if (line_offset_end < line_offset_start) {
		if (line_child_start.type === 'text') {
			oploc = nbe.ops.text(editor, start, end, insertion);
		} else {
			oploc = nbe.ops.link(editor, start, end, insertion);
		}
		ops = ops.concat(oploc.ops);
		if (oploc.loc) {
			loc = oploc.loc;
		}
	} else {
		if (line_child_start) {
			if (line_child_start.type === 'text') {
				oploc = nbe.ops.text(editor, start, null, null);
			} else {
				oploc = nbe.ops.link(editor, start, null, null);
			}
			ops = ops.concat(oploc.ops);
			if (oploc.loc) {
				loc = oploc.loc;
			}
		}

		for (i = line_offset_start; i < line_offset_end; i++) {
			ops = ops.concat(nbe.ops.remove(node.children[i]));
		}

		oploc = null;
		if (line_child_end) {
			if (line_child_end.type === 'text') {
				oploc = nbe.ops.text(editor, null, end, insertion);
			} else {
				oploc = nbe.ops.link(editor, null, end, insertion);
			}
		} else {
			if (insertion) {
				if (line_offset_end === node.children.length) {
					oploc = nbe.ops.append(editor, node.id, insertion);
				} else if (line_offset_end === 0 && end.node.children.length > 0) {
					oploc = nbe.ops.insert_before(editor, end.node.children[0].id, insertion);
				} else {
					oploc = nbe.ops.insert_after(editor, end.node.id, insertion);
				}
			}
		}
		if (oploc) {
			ops = ops.concat(oploc.ops);
			if (oploc.loc) {
				loc = oploc.loc;
			}
		}
	}

	return {ops : ops, loc : loc};
};


nbe.ops.root = function (editor, start, end, insertion) {
	var line_start, line_end, root, root_offset_start, root_offset_end, ops, loc, incorp, conc, new_line_id, parentval, childval, split_point, i, items, merge_point;

	line_start = nbe.location.line(start.node);
	line_end = nbe.location.line(end.node);

	root = line_start.parent;

	root_offset_start = root.children.indexOf(line_start);
	root_offset_end = root.children.indexOf(line_end);

	ops = [];
	loc = null;

	incorp = function (oploc) {
		if (oploc) {
			ops = ops.concat(oploc.ops);
			if (oploc.loc) {
				loc = oploc.loc;
			}
		}
	};

	conc = function (oploc) {
		if (oploc) {
			ops = ops.concat(oploc.ops);
		}
	};

	if (root_offset_start === root_offset_end) {
		if (insertion === null) {
			incorp(nbe.ops.line(editor, start, end, null));
		} else if (insertion.length === 1) {
			incorp(nbe.ops.line(editor, start, end, insertion[0].children));
		} else {
			conc(nbe.ops.line(editor, start, end, insertion[0].children));
			new_line_id = editor.new_id();
			split_point = nbe.location.split_merge_point(end);
			parentval = nbe.lib.clone(line_start.val);
			childval = nbe.state.copy_line_format(editor.format, {});
			if (start.node === line_start) {
				delete parentval.heading;
			} else {
				delete childval.heading;
			}
			ops.push({domop : 'split', parent : line_start.id, child : new_line_id, point : split_point, parentval : parentval, childval : childval});
			loc = {container : new_line_id, offset : 0};
			if (split_point) {
				incorp(nbe.ops.insert_before(editor, split_point, insertion[insertion.length - 1].children));
			} else {
				incorp(nbe.ops.append(editor, new_line_id, insertion[insertion.length - 1].children));
			}
			conc(nbe.ops.insert_before(editor, new_line_id, insertion.slice(1, insertion.length - 1)));
		}
	} else {
		for (i = root_offset_start + 1; i < root_offset_end; i++) {
			ops = ops.concat(nbe.ops.remove(root.children[i]));
		}

		if (insertion === null) {
			incorp(nbe.ops.line(editor, start, null, null));
			conc(nbe.ops.line(editor, null, end, null));
			ops.push({domop : 'merge', parent : line_start.id, child : line_end.id, point : nbe.location.split_merge_point(end), parentval : line_start.val, childval : line_end.val});
		} else if (insertion.length === 1) {
			incorp(nbe.ops.line(editor, start, null, null));
			items = insertion[0].children;
			incorp(nbe.ops.line(editor, null, end, items));
			merge_point = items.length === 0 ? nbe.location.split_merge_point(end) : items[0].id;
			ops.push({domop : 'merge', parent : line_start.id, child : line_end.id, point : merge_point, parentval : line_start.val, childval : line_end.val});
		} else {
			conc(nbe.ops.line(editor, start, null, insertion[0].children));
			conc(nbe.ops.insert_before(editor, line_end.id, insertion.slice(1, insertion.length - 1)));
			incorp(nbe.ops.line(editor, null, end, insertion[insertion.length - 1].children));
		}
	}

	return {ops : ops, loc : loc};
};


nbe.ops.modified = function (editor, ids) {
	var nodes, traverse_remove_mutate, in_dom, removed, mutate, traverse_insert, traverse_line, find_loc, ops, i, loc, oploc;

	nodes = editor.state.nodes;

	traverse_remove_mutate = function (id, ops) {
		var node, i, child;

		node = nodes[id];
		for (i = 0; i < node.children.length; i++) {
			child = node.children[i];
			if (removed(child.id)) {
				ops = ops.concat(nbe.ops.remove(child));
			} else if (child.type === 'text') {
				ops = mutate(child, ops);
			} else if (child.type === 'link') {
				ops = traverse_remove_mutate(child.id, ops);
			}
		}

		return ops;
	};

	in_dom = function (id) {
		var el;

		el = editor.dom[id];
		while (el !== null && !(el.getAttribute && el.getAttribute('data-id') === 'root')) {
			el = el.parentNode;
		}

		return el !== null;
	};

	removed = function (id) {
		if (!in_dom(id)) {
			return true;
		}

		if (nodes[id].type === 'text') {
			return editor.dom[id].textContent === '';
		} else {
			return false;
		}
	};

	mutate = function (node, ops) {
		var el, op;

		el = editor.dom[node.id];
		if (node.val.text !== el.textContent) {
			op = {domop : 'mutate', id : node.id, before : node.val, after : nbe.lib.clone(node.val)};
			op.after.text = el.textContent;
			ops.push(op);
		}

		return ops;
	};

	traverse_insert = function (id, ops) {
		var el, next_id, previous_id, new_val, i, child, text, val, new_id, op, insert_id;

		if (removed(id)) {
			return ops;
		}

		el = editor.dom[id];

		next_id = function (el, index) {
			var el2;

			if (el.childNodes.length === index) {
				return null;
			} else {
				el2 = el.childNodes[index];
				if (el2.getAttribute && el2.getAttribute('data-id')) {
					id = el2.getAttribute('data-id');
					if (nodes[id].type === 'text' && el2.textContent === '') {
						return next_id(el, index + 1);
					} else {
						return id;
					}
				} else {
					return next_id(el, index + 1);
				}
			}
		};

		previous_id = function (el, index) {
			var el2;

			if (index === -1) {
				return null;
			} else {
				el2 = el.childNodes[index];
				if (el2.getAttribute && el2.getAttribute('data-id')) {
					return el2.getAttribute('data-id');
				} else {
					return previous_id(el, index - 1);
				}
			}
		};

		new_val = function (el, index) {
			var val, prev, node, next;

			val = null;
			prev = previous_id(el, index);
			if (prev) {
				node = nodes[prev];
				if (node.type === 'text') {
					val = nbe.lib.clone(node.val);
				}
			}
			if (val === null) {
				next = next_id(el, index);
				if (next) {
					node = nodes[next];
					if (node.type === 'text') {
						val = nbe.lib.clone(node.val);
					}
				}
			}

			return val === null ? {} : val;
		};

		for (i = 0; i < el.childNodes.length; i++) {
			child = el.childNodes[i];
			if (!(child.classList && child.classList.contains('nbe'))) {
				text = child.textContent;
				if (text !== '') {
					val = new_val(el, i);
					val.text = text;
					new_id = editor.new_id();
					op = {id : new_id, type : 'text', val : val};
					insert_id = next_id(el, i);
					if (insert_id) {
						op.domop = 'insert';
						op.before = insert_id;
					} else {
						op.domop = 'append';
						op.parent = id;
					}
					ops.push(op);
				}
			}
		}

		return ops;
	};

	traverse_line = function (id, ops) {
		var node, i, child;

		node = nodes[id];

		ops = traverse_remove_mutate(id, ops);
		ops = traverse_insert(id, ops);
		for (i = 0; i < node.children.length; i++) {
			child = node.children[i];
			if (child.type === 'link') {
				ops = traverse_insert(child.id, ops);
			}
		}

		return ops;
	};

	find_loc = function () {
		var loc, node, el;

		loc = null;
		if (editor.location) {
			loc = {container : editor.location.start.container, offset : editor.location.start.offset};
			if (!removed(loc.container)) {
				node = nodes[loc.container];
				if (node.type === 'text') {
					el = editor.dom[loc.container];
					loc.offset = Math.min(loc.offset + 1, el.textContent.length);
				}
			} else {
				loc = null;
			}
		}

		return loc;
	};

	ops = [];
	for (i = 0; i < ids.length; i++) {
		ops = traverse_line(ids[i], ops);
	}
	loc = find_loc();

	if (loc) {
		oploc = {ops : ops, loc : loc};
	} else {
		oploc = {ops : ops, loc_after : null};
	}

	return oploc;
};


nbe.events.add_event_listeners = function (editor) {
	var el_editor;

	el_editor = editor.el_editor;

	el_editor.addEventListener('click', function (event) {
		//console.log('click');
		nbe.location.get_format(editor);
	}, false);

	el_editor.addEventListener('touchend', function (event) {
		setTimeout(function () {
			nbe.location.get_format(editor);
		}, 0);
	}, false);

	el_editor.addEventListener('keydown', function (event) {
		//console.log('keydown', event);
		if (event.which && (event.keyCode >= 37 && event.keyCode <= 40)) {
			nbe.location.get_format(editor);
		} else if (event.keyCode === 8) {
			editor.trigger('delete', null);
			event.preventDefault();
		} else if (event.keyCode === 9) {
			editor.trigger('tab', null);
			event.preventDefault();
		} else if (event.keyCode === 13) {
			editor.trigger('newline', null);
			event.preventDefault();
		} else if (event.ctrlKey || event.metaKey) {
			if (event.keyCode === 65) {
				editor.trigger('select', null);
				event.preventDefault();
			} else if (event.keyCode === 86) {
				editor.trigger('paste', null);
			} else if (event.keyCode === 88) {
				//editor.trigger('cut', null); cut event is fired automatically.
			} else if (event.keyCode === 90) {
				editor.trigger('undo', event.shiftKey ? 'redo' : 'undo');
				event.preventDefault();
			}
		}
	}, false);

	el_editor.addEventListener('keypress', function (event) {
		var char;

		//console.log('keypress', event);
		if (event.charCode === 0 && event.keyCode >= 37 && event.keyCode <= 40) {
			nbe.location.get_format(editor);
		} else if (!event.ctrlKey && !event.metaKey && event.keyCode !== 8 && event.keyCode !== 9 && event.keyCode !== 13) {
			char = String.fromCharCode(event.charCode ? event.charCode : event.which);
			editor.trigger('text', char);
			event.preventDefault();
		}
	}, false);

	el_editor.addEventListener('keyup', function (event) {
		//console.log('keyup');
		if (event.keyCode >= 37 && event.keyCode <= 40) {
			nbe.location.get_format(editor);
		}
	}, false);

	el_editor.addEventListener('mousedown', function (event) {
		// console.log('mousedown');
	}, false);

	el_editor.addEventListener('mouseup', function (event) {
		nbe.location.get_format(editor);
	}, false);

	el_editor.addEventListener('mouseout', function (event) {
	}, false);

	el_editor.addEventListener('focus', function (event) {
		//console.log('focus');
		editor.focus = true;
	}, false);

	el_editor.addEventListener('blur', function (event) {
		editor.focus = false;
	}, false);

	el_editor.addEventListener('select', function (event) {
		editor.trigger('select', null);
	}, false);

	el_editor.addEventListener('paste', function (event) {
		editor.trigger('paste', null);
	}, false);

	el_editor.addEventListener('cut', function (event) {
		editor.trigger('cut', null);
	}, false);

	editor.mutation = nbe.events.observer(editor);
	if (!editor.mutation.supported) {
		editor.mutation = nbe.events.subtree(editor);
	}
};


nbe.events.observer = function (editor) {
	var MutationObserver, supported, observer, config, observe, disconnect;

	MutationObserver = window.MutationObserver || window.WebKitMutationObserver || window.MozMutationObserver;

	supported = typeof(MutationObserver) !== 'undefined';

	if (supported) {
		observer = new MutationObserver(function (mutations) {
			editor.trigger('observer', mutations);
		});
	}

	config = {childList: true, characterData: true, subtree : true};

	observe = function () {
		observer.observe(editor.el_editor, config);
	};

	disconnect = function () {
		observer.disconnect();
	};

	return {observe : observe, disconnect : disconnect, supported : supported};
};


nbe.events.subtree = function (editor) {
	var active, events, timer, observe, disconnect;

	active = false;
	events = [];
	timer = null;

	editor.el_editor.addEventListener('DOMSubtreeModified', function (event) {
		if (active) {
			events.push(event);
			if (!timer) {
				timer = setTimeout(function () {
					editor.trigger('subtree', events);
					timer = null;
					events = [];
				}, 0);
			}
		}
	}, false);

	observe = function () {
		active = true;
	};

	disconnect = function () {
		active = false;
	};

	return {observe : observe, disconnect : disconnect, supported : true};
};


nbe.triggers.trigger = function (editor, type, value) {
	var oploc, loc_after;

	//console.log('trigger', type, value);
	//nbe.location.get(editor);

	switch (type) {
	case 'text':
		oploc = nbe.triggers.text(editor, value);
		break;
	case 'insertion':
		oploc = nbe.triggers.insertion(editor, value);
		break;
	case 'bold':
	case 'underline':
	case 'italic':
	case 'strikethrough':
	case 'color':
	case 'background_color':
	case 'font_family':
	case 'vertical_align':
	case 'font_size':
	case 'heading':
	case 'text_align':
	case 'line_spacing':
	case 'list':
		oploc = nbe.triggers.format(editor, type, value);
		break;
	case 'left_margin':
		oploc = nbe.triggers.left_margin(editor, value);
		break;
	case 'tab':
		oploc = nbe.triggers.tab(editor);
		break;
	case 'delete':
		oploc = nbe.triggers.del(editor);
		break;
	case 'newline':
		oploc = nbe.triggers.newline(editor);
		break;
	case 'img':
		oploc = nbe.triggers.img(editor, value);
		break;
	case 'link':
		oploc = nbe.triggers.link(editor, value);
		break;
	case 'cut':
		nbe.triggers.cut(editor);
		oploc = 'break';
		break;
	case 'paste':
		nbe.triggers.paste(editor);
		oploc = 'break';
		break;
	case 'undo':
		editor.undo.trigger('undo', value);
		oploc = null;
		break;
	case 'observer':
		oploc = nbe.triggers.observer(editor, value);
		break;
	case 'subtree':
		oploc = nbe.triggers.subtree(editor, value);
		break;
	case 'select':
		nbe.triggers.select(editor);
		oploc = 'break';
		break;
	default:
		oploc = null;
		break;
	}

	//console.log(oploc);

	if (oploc === 'break') {
		return oploc;
	} else if (oploc === null || oploc.ops.length === 0) {
		return null;
	} else {
		loc_after = 'loc_after' in oploc ? oploc.loc_after : {start : oploc.loc, collapsed : true};
		return {ops : oploc.ops, loc_before : editor.location, loc_after : loc_after};
	}
};


nbe.triggers.format = function (editor, type, value) {
	nbe.state.set_format(type, value, editor.format);
	if (editor.location === null) {
		return null;
	} else if (editor.location.collapsed) {
		return nbe.triggers.format_collapsed(editor, type, value);
	} else if (nbe.state.formats.text.indexOf(type) !== -1) {
		return nbe.triggers.text_format(editor, type, value);
	} else {
		return nbe.triggers.line_format(editor, type, value);
	}
};


nbe.triggers.format_collapsed = function (editor, type, value) {
	var line, ops, op, text_nodes, i, text_node;

	line = nbe.location.parent_line(editor, editor.location.start.container);

	ops = [];

	if (!nbe.state.cmp_value_format(type, value, line.val) && ((nbe.state.formats.text.indexOf(type) !== -1 && line.children.length === 0) || (nbe.state.formats.line.indexOf(type) !== -1))) {
		op = {domop : 'mutate', id : line.id, before : line.val};
		op.after = nbe.state.set_format(type, value, nbe.state.copy_line_format(line.val, {}));
		ops.push(op);

		if (type === 'heading' && value !== 'none') {
			text_nodes = nbe.location.text_nodes_in_line(line);
			for (i = 0; i < text_nodes.length; i++) {
				text_node = text_nodes[i];
				if (!nbe.state.cmp_value_format('font_size', nbe.state.formats.default_values.font_size, text_node.val)) {
					op = {domop : 'mutate', id : text_node.id, before : text_node.val};
					op.after = nbe.state.set_format('font_size', nbe.state.formats.default_values.font_size, nbe.state.copy_text_format(text_node.val, {}));
					op.after.text = text_node.val.text;
					ops.push(op);
				}
			}

			delete op.after.list;
		}
	}

	return {ops : ops, loc_after : editor.location};
};


nbe.triggers.text_format = function (editor, type, value) {
	var nodes, start, end, loc_after, ops_split, ops_middle, ops_lines, ops, loc;

	nbe.state.set_format(type, value, editor.format);
	if (editor.location === null || editor.location.collapsed) {
		return null;
	}

	nodes = editor.state.nodes;
	start = editor.location.start;
	end = editor.location.end;

	loc_after = {start : start, end : end, collapsed : false};

	ops_split = function (id, offset_start, offset_end_arg) {
		var ops, node, offset_end, op_mutate, op_start, op_end;

		ops = [];
		node = nodes[id];
		if (node.type === 'text' && !nbe.state.cmp_value_format(type, value, node.val)) {
			offset_end = offset_end_arg === 'infinite' ? node.val.text.length : offset_end_arg;
			if (offset_start !== offset_end) {
				op_mutate = {domop : 'mutate', id : id, before : node.val};
				op_mutate.after = nbe.state.set_format(type, value, nbe.state.copy_text_format(node.val, {}));
				op_mutate.after.text = node.val.text.slice(offset_start, offset_end);
				ops.push(op_mutate);
				if (offset_end_arg !== 'infinite') {
					loc_after.end = {container : id, offset : offset_end - offset_start};
				}
				if (offset_start > 0) {
					op_start = {domop : 'insert', id : editor.new_id(), before : id, type : 'text', val : nbe.state.copy_text_format(node.val, {})};
					op_start.val.text = node.val.text.slice(0, offset_start);
					ops.push(op_start);
					loc_after.start = {container : op_start.id, offset : offset_start};
				}
				if (offset_end < node.val.text.length) {
					op_end = nbe.location.insert_after(editor, id);
					op_end.id = editor.new_id();
					op_end.type = 'text';
					op_end.val = nbe.state.copy_text_format(node.val, {});
					op_end.val.text = node.val.text.slice(offset_end);
					ops.push(op_end);
				}
			}
		}

		return ops;
	};

	ops_middle = function (start_id, end_id) {
		var ops, node, op_mutate;

		ops = [];
		node = nbe.location.previous_node(nodes[end_id]);
		while (node && node.id !== start_id) {
			if (node.type === 'text' && !nbe.state.cmp_value_format(type, value, node.val)) {
				op_mutate = {domop : 'mutate', id : node.id, before : node.val};
				op_mutate.after = nbe.state.set_format(type, value, nbe.state.copy_text_format(node.val, {}));
				op_mutate.after.text = node.val.text;
				ops.push(op_mutate);
			}
			node = nbe.location.previous_node(node);
		}

		return ops;
	};

	ops_lines = function (_start_id, _end_id) {
		var lines, ops;

		lines = nbe.location.lines(editor);

		ops = [];

		lines.forEach(function (node) {
			var op;

			if (!nbe.state.cmp_value_format(type, value, node.val)) {
				op = {domop : 'mutate', id : node.id, before : node.val};
				op.after = nbe.state.set_format(type, value, nbe.state.copy_line_format(node.val, {}));
				ops.push(op);
			}
		});

		return ops;
	};

	if (start.container === end.container) {
		ops = ops_split(start.container, start.offset, end.offset);
		loc = {container : start.container, offset : end.offset - start.offset};
	} else {
		ops = ops_split(start.container, start.offset, 'infinite');
		ops = ops.concat(ops_split(end.container, 0, end.offset));
		ops = ops.concat(ops_middle(start.container, end.container));
		ops = ops.concat(ops_lines(start.container, end.container));
		loc = end;
	}

	return {ops : ops, loc_after : loc_after};
};


nbe.triggers.line_format = function (editor, type, value) {
	var lines, ops;

	lines = nbe.location.lines(editor);

	ops = [];
	lines.forEach(function (node) {
		var op;

		if (!nbe.state.cmp_value_format(type, value, node.val)) {
			op = {domop : 'mutate', id : node.id, before : node.val};
			op.after = nbe.state.set_format(type, value, nbe.state.copy_line_format(node.val, {}));
			ops.push(op);

			if (type === 'heading' && value !== 'none') {
				nbe.location.text_nodes_in_line(node).forEach(function (text_node) {
					if (!nbe.state.cmp_value_format('font_size', nbe.state.formats.default_values.font_size, text_node.val)) {
						op = {domop : 'mutate', id : text_node.id, before : text_node.val};
						op.after = nbe.state.set_format('font_size', nbe.state.formats.default_values.font_size, nbe.state.copy_text_format(text_node.val, {}));
						op.after.text = text_node.val.text;
						ops.push(op);
					}
				});

				delete op.after.list;
			}
		}
	});

	return {ops : ops, loc_after : editor.location};
};


nbe.triggers.left_margin = function (editor, value) {
	var lines, ops;

	if (editor.location === null) {
		return null;
	}

	lines = nbe.location.lines(editor);

	ops = [];

	lines.forEach(function (node) {
		var margin_pre, margin_post, op;

		margin_pre = 'left_margin' in node.val ? node.val.left_margin : 0;
		margin_post = margin_pre + (value === 'increment' ? 1 : -1) * nbe.state.formats.left_margin.step;
		if (margin_post >= 0 && margin_post <= nbe.state.formats.left_margin.max) {
			op = {domop : 'mutate', id : node.id, before : node.val};
			op.after = nbe.state.set_format('left_margin', margin_post, nbe.state.copy_line_format(node.val, {}));
			ops.push(op);
		}
	});

	return {ops : ops, loc_after : editor.location};
};


nbe.triggers.text = function (editor, text) {
	var location, start, end, val, insertion;

	if (!editor.location) {
		return null;
	}

	location = editor.location;

	if (location.collapsed) {
		return nbe.triggers.text_collapsed(editor, text);
	} else {
		start = nbe.location.loc_to_point(editor, location.start);
		end = nbe.location.loc_to_point(editor, location.end);
		val =  nbe.state.copy_text_format(editor.format, {});
		val.text = text;
		insertion = [{type : 'line', val : {}, children : [{type : 'text', val : val, children : []}]}];
		return nbe.ops.root(editor, start, end, insertion);
	}
};


nbe.triggers.text_collapsed = function (editor, text) {
	var max_text_length, start, node, op, val, insertion;

	max_text_length = 10;

	start = nbe.location.loc_to_point(editor, editor.location.start);
	node = start.node;

	if (node.type === 'text' && node.val.text.length < max_text_length && (start.offset < node.val.text.length || node.parent.type === 'line') && nbe.state.cmp_text_format(node.val, editor.format)) {
		op = {domop : 'mutate', id : node.id, before : node.val, after : nbe.state.copy_text_format(node.val, {})};
		op.after.text = node.val.text.slice(0, start.offset) + text + node.val.text.slice(start.offset);

		return {ops : [op], loc : {container : node.id, offset : start.offset + text.length}};
	} else {
		val =  nbe.state.copy_text_format(editor.format, {});
		val.text = text;
		insertion = [{type : 'line', val : {}, children : [{type : 'text', val : val, children : []}]}];

		return nbe.ops.root(editor, start, start, insertion);
	}
};


nbe.triggers.del = function (editor) {
	var location, node, loc_start, start, end;

	if (!editor.location) {
		return null;
	}

	location = editor.location;
	node = editor.state.nodes[location.start.container];

	if (node.type === 'line' && 'left_margin' in node.val && location.collapsed) {
		return nbe.triggers.left_margin(editor, 'decrement');
	} else if (location.collapsed) {
		loc_start = nbe.location.previous_location(editor, location.start);
		start = nbe.location.loc_to_point(editor, loc_start);
		end = nbe.location.loc_to_point(editor, location.start);
	} else {
		start = nbe.location.loc_to_point(editor, location.start);
		end = nbe.location.loc_to_point(editor, location.end);
	}

	return nbe.ops.root(editor, start, end, null);
};


nbe.triggers.tab = function (editor) {
	var node, oploc;

	if (!editor.location) {
		return null;
	}

	node = editor.state.nodes[editor.location.start.container];
	if (node.type === 'line') {
		oploc = nbe.triggers.left_margin(editor, 'increment');
	} else {
		oploc = nbe.triggers.text(editor, ' ');
	}

	return oploc;
};


nbe.triggers.newline = function (editor) {
	var location, start, end, insertion;

	if (!editor.location) {
		return null;
	}

	location = editor.location;

	if (location.collapsed) {
		start = end = nbe.location.loc_to_point(editor, location.start);
	} else {
		start = nbe.location.loc_to_point(editor, location.start);
		end = nbe.location.loc_to_point(editor, location.end);
	}

	insertion = [{type : 'line', val : {}, children : []}, {type : 'line', val : {}, children : []}];

	return nbe.ops.root(editor, start, end, insertion);
};


nbe.triggers.img = function (editor, value) {
	var node, op, oploc, location, start, end, val, insertion;

	if ('id' in value && value.id in editor.state.nodes) {
		node = editor.state.nodes[value.id];
		op = {domop : 'mutate', id : value.id, before : node.val, after : nbe.lib.clone(value)};
		delete op.after.id;
		oploc = {ops : [op], loc_after : editor.location};
	} else if (!editor.location) {
		oploc = null;
	} else {
		location = editor.location;

		if (location.collapsed) {
			start = end = nbe.location.loc_to_point(editor, location.start);
		} else {
			start = nbe.location.loc_to_point(editor, location.start);
			end = nbe.location.loc_to_point(editor, location.end);
		}

		val = nbe.lib.clone(value);
		insertion = [{type : 'line', val : {}, children : [{type : 'img', val : val, children : []}]}];

		oploc = nbe.ops.root(editor, start, end, insertion);
	}

	return oploc;
};


nbe.triggers.link = function (editor, value) {
	var node, op, oploc, location, start, end, link, insertion;

	if ('id' in value && value.id in editor.state.nodes) {
		node = editor.state.nodes[value.id];
		op = {domop : 'mutate', id : value.id, before : node.val, after : {href : value.href}};
		oploc = {ops : [op], loc_after : editor.location};
	} else if (!editor.location) {
		oploc = null;
	} else {
		location = editor.location;

		if (location.collapsed) {
			start = end = nbe.location.loc_to_point(editor, location.start);
		} else {
			start = nbe.location.loc_to_point(editor, location.start);
			end = nbe.location.loc_to_point(editor, location.end);
		}

		link = {type : 'link', val : {href : value.href}, children : value.insertion};
		insertion = [{type : 'line', val : {}, children : [link]}];

		oploc = nbe.ops.root(editor, start, end, insertion);
	}

	return oploc;
};


nbe.triggers.paste = function (editor) {
	var callback;

	callback = function (insertion) {
		editor.trigger('insertion', insertion);
	};

	nbe.paste.clipboard(callback);
};


nbe.triggers.cut = function (editor) {
	editor.mutation.disconnect();
	setTimeout(function () {
		nbe.state.clean(editor);
		if (!editor.location.collapsed) {
			editor.trigger('delete', null);
		}
		editor.mutation.observe();
	}, 0);
};


nbe.triggers.select = function (editor) {
	var last, next, offset, location;

	last = nbe.location.last_child(editor.state.nodes.root);
	next = nbe.location.next_node(last);
	while (next !== null) {
		last = next;
		next = nbe.location.next_node(last);
	}

	if (last.type === 'text') {
		offset = last.val.text.length;
	} else if (last.type === 'line') {
		offset = 0;
	} else {
		offset = 1;
	}

	location = {start : {container : 'line', offset : 0}, end : {container : last.id, offset : offset}, collapsed : false};

	nbe.location.set(editor, location);
};


nbe.triggers.insertion = function (editor, insertion) {
	var location, start, end;

	if (!editor.location) {
		return null;
	}

	location = editor.location;

	if (location.collapsed) {
		start = end = nbe.location.loc_to_point(editor, location.start);
	} else {
		start = nbe.location.loc_to_point(editor, location.start);
		end = nbe.location.loc_to_point(editor, location.end);
	}

	return nbe.ops.root(editor, start, end, insertion);
};


nbe.triggers.observer = function (editor, mutations) {
	var nodes, dom, added_nodes, removed_nodes, mutated_nodes, add_to_array, remove_from_array, add_node, remove_node, mutate_node, add_line, lines, oploc;

	nodes = editor.state.nodes;
	dom = editor.dom;
	added_nodes = [];
	removed_nodes = [];
	mutated_nodes = [];

	add_to_array = function (array, item) {
		var index;

		index = array.indexOf(item);
		if (index === -1) {
			array.push(item);
		}

		return index === -1;
	};

	remove_from_array = function (array, item) {
		var index;

		index = array.indexOf(item);
		if (index !== -1) {
			array.splice(index, 1);
		}

		return index !== -1;
	};

	add_node = function (node) {
		add_to_array(added_nodes, node);
	};

	remove_node = function (node) {
		var removed;

		removed = remove_from_array(added_nodes, node);
		if (!removed) {
			add_to_array(removed_nodes, node);
		}
	};

	mutate_node = function (node) {
		if (added_nodes.indexOf(node) === -1) {
			add_to_array(mutated_nodes, node);
		}
	};

	mutations.forEach(function (mutation) {
		var i;

		if (mutation.type === 'characterData') {
			mutate_node(mutation.target);
		} else if (mutation.type === 'childList') {
			for (i = 0; i < mutation.addedNodes.length; i++) {
				add_node(mutation.addedNodes[i]);
			}
			for (i = 0; i < mutation.removedNodes.length; i++) {
				remove_node(mutation.removedNodes[i]);
			}
		}
	});

	add_line = function (el, lines) {
		var id;

		while (el !== null && !(el.classList && el.classList.contains('line'))) {
			el = el.parentNode;
		}

		if (el) {
			id = el.getAttribute('data-id');
			lines[id] = true;
		}
	};

	lines = {};

	added_nodes.concat(removed_nodes).concat(mutated_nodes).forEach(function (node) {
		add_line(node, lines);
	});

	oploc = nbe.ops.modified(editor, Object.keys(lines));

	nbe.state.clean(editor);

	return oploc;
};


nbe.triggers.subtree = function (editor, events) {
	var find_line, lines, i, oploc;

	find_line = function (el, lines) {
		while (el !== null && !(el.classList && el.classList.contains('line'))) {
			el = el.parentNode;
		}

		if (el !== null) {
			lines[el.getAttribute('data-id')] = true;
		}

		return lines;
	};

	lines = {};
	for (i = 0; i < events.length; i++) {
		find_line(events[i].target ? events[i].target : null, lines);
	}

	oploc = nbe.ops.modified(editor, Object.keys(lines));

	nbe.state.clean(editor);

	return oploc;
};


nbe.editor.create = function (editor_id, options, doc) {
	var el_editor, add_external_ops, init, editor;

	el_editor = document.createElement('div');
	el_editor.classList.add('wu-editor');
	el_editor.setAttribute('data-id', 'editor');

	add_external_ops = function (ops, set_location) {
		ops = ops.filter(function (op) {
			return !('editor_class' in op);
		});
		nbe.state.update(editor, editor.state, editor.dom, ops);
		if (editor.focus && set_location) {
			nbe.location.set(editor, editor.location);
		}
	};

	init = function (state) {
		nbe.state.init(editor, state);
		editor.location = null;
	};

	editor = {
		id : editor_id,
		state : null,
		dom : null,
		location : null,
		format : {},
		inputs : null,
		undo : null,
		trigger : null,
		el_editor : el_editor,
		get_html : function () {
			return el_editor.innerHTML;
		},
		init : init,
		focus : false,
		add_internal_oploc : null,
		add_external_ops : add_external_ops,
		new_id : null,
		mutation : {observe : function () {}, disconnect : function () {}}
	};

	if (options.editable) {
		el_editor.contentEditable = true;
		editor.new_id = nbe.lib.new_id();
		editor.inputs = nbe.notify.inputs(editor);
		editor.undo = nbe.editor.undo(editor);
		editor.observer = nbe.events.observer(editor);
		editor.add_internal_oploc = function (oploc) {
			doc.add_ops(editor_id, oploc.ops);
			nbe.state.update(editor, editor.state, editor.dom, oploc.ops);
			nbe.location.set(editor, oploc.loc_after);
			nbe.location.format_update(editor);
		};
		editor.trigger = function (type, value) {
			var oploc;

			editor.focus = true;
			oploc = nbe.triggers.trigger(editor, type, value);
			if (oploc !== null && oploc !== 'break') {
				editor.add_internal_oploc(oploc);
				editor.undo.add_oploc(oploc);
			} else if (oploc === null) {
				nbe.location.set(editor, editor.location);
				editor.inputs.notify();
			}
		};

		nbe.events.add_event_listeners(editor);
	}

	return editor;
};


nbe.editor.undo = function (editor) {
	var undoes, redoes, buttons, add_button, remove_button, notify_buttons, add_oploc, trigger;

	undoes = [];
	redoes = [];

	buttons = [];

	add_button = function (button) {
		buttons.push(button);
		notify_buttons();
	};

	remove_button = function (button) {
		var index;

		index = buttons.indexOf(button);
		if (index !== -1) {
			buttons = buttons.splice(index, 1);
		}
	};

	notify_buttons = function () {
		var value, i;

		value = {undo : undoes.length !== 0, redo : redoes.length !== 0};
		for (i = 0; i < buttons.length; i++) {
			buttons[i].set_value(value);
		}
	};

	add_oploc = function (oploc) {
		undoes.push(oploc);
		redoes = [];
		notify_buttons();
	};

	trigger = function (type, value) {
		var oploc, oploc_inv;

		if (value === 'undo' && undoes.length !== 0) {
			oploc = undoes.pop();
			redoes.push(oploc);
			oploc_inv = nbe.state.invert_oploc(oploc);
			editor.add_internal_oploc(oploc_inv);
			nbe.location.format_update(editor);
		} else if (value === 'redo' && redoes.length !== 0) {
			oploc = redoes.pop();
			undoes.push(oploc);
			editor.add_internal_oploc(oploc);
		}
		notify_buttons();
	};

	return {add_button : add_button, remove_button : remove_button, add_oploc : add_oploc, trigger : trigger};
};


nbe.notify.inputs = function (editor) {
	var inputs, add, remove, notify, notify_type;

	inputs = {};

	add = function (type, input) {
		if (type in inputs && inputs[type].indexOf(input) === -1) {
			inputs[type].push(input);
		} else {
			inputs[type] = [input];
		}
	};

	remove = function (type, input) {
		var inputs_type, index;

		inputs_type = inputs[type];
		if (inputs_type) {
			index = inputs_type.indexOf(input);
			if (index !== -1) {
				inputs[type] = inputs_type.slice(0, index).concat(inputs_type.slice(index + 1));
			}
		}
	};

	notify_type = function (type, value) {
		var i;

		if (type === 'left_margin' && 'left_margin' in inputs) {
			value = nbe.notify.left_margin(editor);
		}

		for (i = 0; i < (type in inputs ? inputs[type].length : 0) ; i++) {
			inputs[type][i].set_value(value);
		}
	};

	notify = function () {
		var type;

		for (type in nbe.state.formats.default_values) {
			if (nbe.state.formats.default_values.hasOwnProperty(type)) {
				notify_type(type, type in editor.format ? editor.format[type] : nbe.state.formats.default_values[type]);
			}
		}
	};

	return {add : add, remove : remove, notify : notify};
};


nbe.notify.left_margin = function (editor, format) {
	var dec, inc, lines;

	dec = 'off';
	inc = 'off';

	lines = nbe.location.lines(editor);
	lines.forEach(function (line) {
		var margin;

		margin = 'left_margin' in line.val ? line.val.left_margin : 0;
		inc = margin < nbe.state.formats.left_margin.max ? 'on' : inc;
		dec = margin > 0 ? 'on' : dec;
	});

	return dec + ':' + inc;
};


nbe.paste.clipboard = function (callback) {
	var container, range, selection;

	container = document.createElement('div');
	container.contentEditable = true;
	container.className = 'clipboard';

	range = document.createRange();
	range.setStart(container, 0);
	range.setEnd(container, 0);
	selection = window.getSelection();
	selection.removeAllRanges();
	selection.addRange(range);
	document.body.appendChild(container);
	container.focus();

	setTimeout(function () {
		var insertion;

		insertion = nbe.paste.insertion(container);
		document.body.removeChild(container);
		callback(insertion);
	}, 0);
};


nbe.paste.insertion = function (container) {
	var line, state, insertion;

	line = {type : 'line', val : {}, children : []};
	state = {root : [line], line : line, link : null, format : {}};

	state = nbe.paste.traverse(state, container);

	insertion = [];

	if (Object.keys(state.root[0].val).length !== 0) {
		insertion.push({type : 'line', val : {}, children : []});
	}

	insertion = insertion.concat(state.root);

	if (Object.keys(state.root[state.root.length - 1].val).length !== 0) {
		insertion.push({type : 'line', val : {}, children : []});
	}

	return insertion;
};


nbe.paste.traverse = function (state, node) {
	var i, child;

	for (i = 0; i < node.childNodes.length; i++) {
		child = node.childNodes[i];
		switch (child.nodeName) {
		case 'DIV':
		case 'div':
		case 'P':
		case 'p':
		case 'H1':
		case 'h1':
		case 'H2':
		case 'h2':
		case 'H3':
		case 'h3':
		case 'H4':
		case 'h4':
		case 'H5':
		case 'h5':
		case 'H6':
		case 'h6':
			state = nbe.paste.div(state, child);
			break;
		case 'SPAN':
		case 'span':
			state = nbe.paste.span(state, child);
			break;
		case 'A':
		case 'a':
			state = nbe.paste.link(state, child);
			break;
		case 'IMG':
		case 'img':
			state = nbe.paste.img(state, child);
			break;
		case '#text':
		case '#TEXT':
			state = nbe.paste.text(state, child);
			break;
		case 'BR':
		case 'br':
			state = nbe.paste.br(state, child);
			break;
		case 'STYLE':
		case 'style':
			break;
		default:
			state = nbe.paste.remaining(state, child);
			break;
		}
	}

	return state;
};


nbe.paste.div = function (state, node) {
	var format, format_div, add_class, left_margin, val, line;

	format = state.format;

	format_div = nbe.lib.clone(format);

	add_class = function (key, names) {
		var i;

		for (i = 0; i < names.length; i++) {
			if (node.classList.contains(names[i])) {
				format_div[key] = names[i];
				return null;
			}
		}
	};

	add_class('text_align', ['center', 'right', 'justify']);
	add_class('heading', ['heading1', 'heading2', 'heading3', 'heading4', 'heading5', 'heading6']);
	add_class('list', ['disc', 'lower-alpha', 'lower-roman', 'square', 'upper-alpha', 'upper-roman', 'ordered']);
	add_class('line_spacing', ['line_spacing_05', 'line_spacing_06', 'line_spacing_07', 'line_spacing_08', 'line_spacing_09', 'line_spacing_10', 'line_spacing_11', 'line_spacing_12', 'line_spacing_13', 'line_spacing_14', 'line_spacing_15', 'line_spacing_16', 'line_spacing_17', 'line_spacing_18', 'line_spacing_19', 'line_spacing_20']);

	if (node.style.marginLeft) {
		left_margin = Number(node.style.marginLeft.slice(0, node.style.marginLeft.length - 2));
		if (left_margin >= 0) {
			format_div.left_margin = left_margin;
		}
	}

	if (node.style.fontSize) {
		format_div.font_size = node.style.fontSize;
	}

	switch (node.align) {
	case 'LEFT':
	case 'left':
		delete format_div.text_align;
		break;
	case 'RIGHT':
	case 'right':
		format_div.text_align = 'right';
		break;
	case 'CENTER':
	case 'center':
		format_div.text_align = 'center';
		break;
	case 'JUSTIFY':
	case 'justify':
		format_div.text_align = 'justify';
		break;
	}

	switch (node.nodeName) {
	case 'H1':
	case 'h1':
		format_div.heading = 'heading1';
		break;
	case 'H2':
	case 'h2':
		format_div.heading = 'heading2';
		break;
	case 'H3':
	case 'h3':
		format_div.heading = 'heading3';
		break;
	case 'H4':
	case 'h4':
		format_div.heading = 'heading4';
		break;
	case 'H5':
	case 'h5':
		format_div.heading = 'heading5';
		break;
	case 'H6':
	case 'h6':
		format_div.heading = 'heading6';
		break;
	}

	val = nbe.state.copy_line_format(format_div, {});

	if (state.line.children.length === 0) {
		state.line.val = val;
	} else {
		line = {type : 'line', val : val, children : []};
		state.root.push(line);
		state.line = line;
	}

	state.format = format_div;

	state = nbe.paste.traverse(state, node);

	state.format = format;

	return state;
};


nbe.paste.span = function (state, node) {
	var format, format_span, add_classes, verify_color, add_styles, font_family;

	format = state.format;

	format_span = nbe.lib.clone(format);

	add_classes = function (names) {
		var i;

		for (i = 0; i < names.length; i++) {
			if (node.classList.contains(names[i])) {
				format_span[names[i]] = 'on';
			}
		}
	};

	add_classes(['bold', 'italic', 'underline', 'strikethrough']);

	verify_color = function (col) {
		return col.slice(0, 4) === 'rgb(';
	};

	if (node.style.color && verify_color(node.style.color)) {
		format_span.color = node.style.color;
	}

	if (node.style.backgroundColor && verify_color(node.style.backgroundColor)) {
		format_span.background_color = node.style.backgroundColor;
	}

	add_styles = function (names) {
		var i;

		for (i = 0; i < names.length; i++) {
			if (node.style[names[i].style]) {
				format_span[names[i].key] = node.style[names[i].style];
			}
		}
	};

	add_styles([
		{key : 'vertical_align', style : 'verticalAlign'}
	]);

	if (format_span.vertical_align) {
		if (node.style.fontSize.slice(-2) === 'px') {
			format_span.font_size = (1.25 * Number(node.style.fontSize.slice(0, node.style.fontSize.length - 2))) + 'px';
		}
	} else {
		add_styles([
			{key : 'font_size', style : 'fontSize'}
		]);
	}

	if (node.style.fontFamily) {
		font_family = node.style.fontFamily.toLowerCase();
		if (nbe.state.formats.font_family.indexOf(font_family) !== -1) {
			format_span.font_family = font_family;
		}
	}

	state.format = format_span;

	state = nbe.paste.traverse(state, node);

	state.format = format;

	return state;
};


nbe.paste.link = function (state, node) {
	var val, item;

	val = {href : node.href};
	item = {type : 'link', val : val, children : []};

	state.line.children.push(item);

	state.link = item;

	state = nbe.paste.traverse(state, node);

	state.link = null;

	return state;
};


nbe.paste.img = function (state, node) {
	var val, add_props, item;

	val = {};

	add_props = function (names) {
		var i;

		for (i = 0; i < names.length; i++) {
			if (node[names[i]]) {
				val[names[i]] = node[names[i]];
			}
		}
	};

	add_props(['src', 'width', 'height', 'title']);

	item = {type : 'img', val : val, children : []};

	if (state.link) {
		state.link.children.push(item);
	} else {
		state.line.children.push(item);
	}

	return state;
};


nbe.paste.text = function (state, node) {
	var val, item;

	val = nbe.state.copy_text_format(state.format, {});
	val.text = node.textContent;

	item = {type : 'text', val : val, children : []};

	if (state.link) {
		state.link.children.push(item);
	} else {
		state.line.children.push(item);
	}

	return state;
};


nbe.paste.br = function (state, node) {
	var line;

	line = {type : 'line', val : {}, children : []};
	state.root.push(line);
	state.line = line;

	return state;
};


nbe.paste.remaining = function (state, node) {
	var format, format_remaining;

	format = state.format;

	format_remaining = nbe.lib.clone(format);

	switch (node.nodeName) {
	case 'STRONG':
	case 'strong':
	case 'B':
	case 'b':
		format_remaining.bold = 'on';
		break;
	case 'I':
	case 'i':
		format_remaining.italic = 'on';
		break;
	case 'U':
	case 'u':
		format_remaining.underline = 'on';
		break;
	}

	state.format = format_remaining;

	state = nbe.paste.traverse(state, node);

	state.format = format;

	return state;
};


kite.browser.dom = {};

kite.browser.dom.eac = function (type, append_to, classname) {
	var element = document.createElement(type);
	element.className = classname;
	append_to.appendChild(element);
	return element;
};

kite.browser.dom.ec = function (type, classname) {
	var element = document.createElement(type);
	element.className = classname;
	return element;
};

kite.browser.dom.ea = function (type, append_to) {
	var element = document.createElement(type);
	append_to.appendChild(element);
	return element;
};

kite.browser.dom.input = function (type, id, name, value, classname, placeholder, append_to) {
	var element, properties, i, p;

	element = document.createElement('input');
	properties = ['type', 'id', 'name', 'value', 'className', 'placeholder'];

	for (i = 0; i < properties.length; i++) {
		p = properties[i];
		if (arguments[i]) {
			element.setAttribute(p, arguments[i]);
		}
	}
	if (append_to) {
		append_to.appendChild(element);
	}
	return element;
};

kite.browser.dom.select_option = function (value, text, el_parent) {
	var el_option;

	el_option = kite.browser.dom.ea('option', el_parent);
	el_option.value = value;
	el_option.innerHTML = text;

	return el_option;
};

kite.browser.dom.removeChildNodes = function (el) {
	while (el.hasChildNodes()) {
		el.removeChild(el.firstChild);
	}
};

kite.browser.dom.has_parent = function (node, parent) {
	while (node.parentNode) {
		if (node.parentNode === parent) {
			return true;
		}
		node = node.parentNode;
	}
	return false;
};

kite.browser.dom.text = function (node, txt) {
	node.appendChild(document.createTextNode(txt));
	return node;
};

kite.browser.dom.svg = function (x, y, width, height, class_name, append_to) {
	var el_svg;

	el_svg = document.createElementNS("http://www.w3.org/2000/svg", "svg");
	el_svg.setAttribute("version", "1.2");
	el_svg.setAttribute("baseProfile", "tiny");
	if (class_name) {
		el_svg.setAttribute('class', class_name);
	}
	if (x) {
		el_svg.setAttribute('x', x + 'px');
	}
	if (y) {
		el_svg.setAttribute('y', y + 'px');
	}
	if (height) {
		el_svg.setAttribute('height', height + 'px');
	}
	if (width) {
		el_svg.setAttribute('width', width + 'px');
	}
	if (height && width) {
		el_svg.setAttribute('viewBox', (x ? x + ' ' : '0 ') + (y ? y + ' ' : '0 ') + ' ' + height + ' ' + width);
	}

	append_to.appendChild(el_svg);

	return el_svg;
};

kite.browser.dom.ns = function (type, append_to, attribute) {
	var element = document.createElementNS("http://www.w3.org/2000/svg", type);
	if (append_to) {
		append_to.appendChild(element);
	}
	if (attribute) {
		element.setAttribute(attribute[0], attribute[1]);
	}
	return element;
};


kite.browser.ui = {};

kite.browser.ui.Window_core = function () {
	var that, move, prev_width, prev_height;

	that = this;

	this.close_handler = null;
	this.close_on = ''; // click/out
	this.is_open = false;
	this.close_function = null;
	this.element = kite.browser.dom.ec('div', 'window window_light');
	this.header = kite.browser.dom.ec('div', 'window_header header_light');
	this.container = kite.browser.dom.ec('div', 'container');

	move = new kite.browser.ui.Move(that.element, {});

	this.header.addEventListener('mousedown', function (e) {
		if (e.target === that.header) {
			move.drag_start(e, {});
		}
	}, false);

	prev_width = document.documentElement.clientWidth;
	prev_height = document.documentElement.clientHeight;

	this.check_dimensions_position = function (e) {
		if (prev_width !== document.documentElement.clientWidth || prev_height !== document.documentElement.clientHeight) {
			that.position();
			prev_width = document.documentElement.clientWidth;
			prev_height = document.documentElement.clientHeight;
		}
	};

	// Default action, run in position()
	this.action = function (el_target, target_position) {
		return true;
	};
};

kite.browser.ui.Window_core.prototype.set_content = function (content) { // Sets window content (this.container)
	//var this_window = this;
	this.container.appendChild(content);
	/*
	this.container.addEventListener('DOMSubtreeModified', function (e) {
		this_window.position();
	}, false);
	*/
};
kite.browser.ui.Window_core.prototype.set_title = function (title) { // Sets window title
	if (this.header !== undefined) {
		kite.browser.dom.text(this.header, title);
	}
};
kite.browser.ui.Window_core.prototype.set_close_handler = function (close_handler) { // Sets custom close handler
	this.close_handler = close_handler;
};
kite.browser.ui.Window_core.prototype.open = function (el_target) { // Display window
	var that = this;

	//if (!this.element.parentNode) {
	kite.browser.ui.set_opacity(this.element, 1);
	if (this.cover) {
		document.body.appendChild(this.cover);
	}

	document.body.appendChild(this.element);

	this.close_function = function (e) {
		if (!kite.browser.dom.is_element_child(that.element, e.target) && !kite.browser.dom.is_element_child(el_target, e.target)) {
			that.close();
		}
	};

	if (this.close_on === 'out') {
		this.element.addEventListener('mouseout', this.close_function, false);
	} else if (this.close_on === 'click') {
		document.body.addEventListener('mousedown', this.close_function, false);
	}

	this.element.style.left = (document.documentElement.clientWidth / 2) - (this.element.offsetWidth / 2) + 'px';

	this.position(el_target);
	this.is_open = true;

	window.addEventListener('resize', this.check_dimensions_position, false);
	document.body.addEventListener('orientationchange', this.check_dimensions_position, false);

	//}
};
kite.browser.ui.Window_core.prototype.size = function () { // Adjust window size to content
/*	var min_width, min_height, width, height, max_width, max_height, current_width, current_height, overflow;

	min_width = this.container.firstChild.offsetWidth;
	min_height = this.container.firstChild.offsetHeight;
	max_width = window.innerWidth - 60;
	max_height = window.innerHeight - 60;
	current_width = this.container.offsetWidth - 10;
	current_height = this.container.offsetHeight - 10;
	overflow = 'visible';

	if (min_height > max_height) {
		min_height = max_height;
		height = max_height + 'px';
		overflow = 'auto';
	} else if (min_height > current_height) {
		height = 'auto';
		overflow = 'visible';
	} else {
		height = current_height + 'px';
	}

	if (min_width > max_width) {
		min_width = max_width;
		width = max_width + 'px';
		overflow = 'auto';
	} else if (min_width > current_width) {
		width = 'auto';
		if (overflow !== 'auto') {
			overflow = 'visible';
		}
	} else {
		width = current_width + 'px';
	}

	this.container.style.minWidth = min_width + 'px';
	this.container.style.minHeight = min_height + 'px';
	this.container.style.width = width;
	this.container.style.height = height;
	this.container.style.maxWidth = max_width + 'px';
	this.container.style.overflow = overflow;
*/

	// Max width
	this.element.style.width = 'auto';
	if (this.element.offsetWidth >= (window.innerWidth - 20)) {
		this.element.style.width = window.innerWidth - 20 + 'px';
	} else {
		this.element.style.width = 'auto';
	}

	// Max height
	this.element.style.height = 'auto';
	if (this.element.offsetHeight >= (document.documentElement.clientHeight - 20)) {
		this.element.style.height = document.documentElement.clientHeight - 20 + 'px';
	} else {
		this.element.style.height = 'auto';
	}
};
kite.browser.ui.Window_core.prototype.position = function (el_target) { // Positions window relative to el_target
	var target_position, left, top;

	this.size();

	if (el_target) { // Position relative to target
		target_position = kite.browser.ui.get_offset(el_target);

		// left
		left = target_position.left + (el_target.offsetWidth / 2) - (this.element.offsetWidth / 2);
		if (left + this.element.offsetWidth > window.innerWidth) {
			this.element.style.left = (window.innerWidth - this.element.offsetWidth) + 'px';
		} else if (left < 0) {
			this.element.style.left = '0px';
		} else {
			this.element.style.left = left + 'px';
		}
		this.action(el_target, target_position);
	} else { // Position relative to screen
		window.scrollTo(0, 0);
		top = (document.documentElement.clientHeight - this.element.offsetHeight) / 2;
		//alert(document.documentElement.clientHeight + ', ' + this.element.offsetHeight + ', ' + top + ', ' + this.element.offsetTop);
		if (top < 0) {
			top = 0;
		}
		this.element.style.top = top + 'px';
		//alert(this.element.offsetTop);
		left = (window.innerWidth - this.element.offsetWidth) / 2;
		if (left < 0) {
			left = 0;
		}
		this.element.style.left = left + 'px';
	}
};
kite.browser.ui.Window_core.prototype.close = function () { // Close without running close handler
	var this_window = this;
	if (this.is_open) {
		kite.browser.animation.Fade_out(this_window.element, { duration : 50, fps: 50, callback : function () {
			document.body.removeChild(this_window.element);
		}});
		if (this_window.cover) {
			document.body.removeChild(this_window.cover);
		}

		if (this.close_on === 'out') {
			this.element.removeEventListener('mouseout', this.close_function, false);
		} else if (this.close_on === 'click') {
			document.body.removeEventListener('mousedown', this.close_function, false);
		}

		this.close_function = null;
		this.is_open = false;

		window.removeEventListener('resize', this.check_dimensions_position, false);
		document.body.removeEventListener('orientationchange', this.check_dimensions_position, false);
	}
};
kite.browser.ui.Window_core.prototype.terminate = function () { // Close and run close handler
	this.close();
	if (this.close_handler !== null) {
		this.close_handler();
	}
};
kite.browser.ui.Window_core.prototype.insert_close_button = function () {
	var that = this;
	this.close_button = kite.browser.dom.eac('img', kite.browser.dom.eac('div', this.header, 'close_div'), 'close_button');
	this.close_button.src = '/public/inlund/img/close.png';
	this.close_button.addEventListener('click', function (e) {
		that.terminate();
	}, false);
};
kite.browser.ui.Window_core.prototype.insert_footer = function (element) { // Insert footer element
	var that, el_resize, resize;
	that = this;
	this.footer = kite.browser.dom.eac('div', element, 'window_footer_light');
	el_resize = kite.browser.dom.eac('img', that.footer, 'window_resize');
	el_resize.src = '/public/inlund/img/resize.png';
	resize = kite.browser.ui.Resize(that.container, {});
	el_resize.addEventListener('mousedown', function (e) {
		resize.drag_start(e, {});
	}, false);
};

kite.browser.ui.Window = function () {
	var that = new kite.browser.ui.Window_core();

//	that.element.appendChild(that.header);
	that.element.appendChild(that.container);
//	that.insert_close_button();
//	that.insert_footer(that.element);

	return that;
};

kite.browser.ui.Dialog = function () {
	var that = new kite.browser.ui.Window_core();

	that.container.className = 'container_dark';
	that.cover = kite.browser.dom.ec('div', 'dialog_cover');
	that.cover.addEventListener('click', function (e) {
		kite.browser.animation.shake(that.element, null);
	}, false);

//	that.element.appendChild(that.header);
	that.element.appendChild(that.container);

	return that;
};

kite.browser.ui.confirm = function (title, text, buttons, callback) {
	var dialog, el_content, el_buttons, i, len, el_button;

	dialog = new kite.browser.ui.Dialog();
	dialog.set_title(title);

	el_content = kite.browser.dom.ec('div', 'confirm_content');
	el_content.textContent = text;
	el_buttons = kite.browser.dom.eac('div', el_content, 'overflow_hidden');
	el_buttons.style.marginTop = '10px';

	for (i = 0, len = buttons.length; i < len; i++) {
		el_button = kite.browser.dom.eac('button', el_buttons, 'float_left');
		el_button.textContent = buttons[i];
		el_button.id = buttons[i];
	}

	dialog.set_content(el_content);

	el_buttons.addEventListener('click', function (e) {
		if (e.target.id) {
			if (callback) {
				callback(e.target.id);
			}
			dialog.close();
		}
	}, false);

	dialog.open();
};

kite.browser.ui.Confirm = function (title, text, buttons, callback) {
	var that, el_content, el_buttons, i, len, el_button;

	that = new kite.browser.ui.Dialog();
	that.set_title(title);

	el_content = kite.browser.dom.ec('div', 'confirm_content');
	el_content.textContent = text;
	el_buttons = kite.browser.dom.eac('div', el_content, 'overflow_hidden');
	el_buttons.style.marginTop = '10px';

	for (i = 0, len = buttons.length; i < len; i++) {
		el_button = kite.browser.dom.eac('button', el_buttons, 'float_left');
		el_button.textContent = buttons[i];
		el_button.id = buttons[i];
	}

	that.set_content(el_content);

	el_buttons.addEventListener('click', function (e) {
		if (e.target.id) {
			if (callback) {
				callback(e.target.id);
			}
			that.close();
		}
	}, false);

	return that;
};

kite.browser.ui.Pop_up = function () {
	var that, el_arrow_space, el_arrow_container, el_arrow;

	that = new kite.browser.ui.Window_core();

	that.close_on = 'click';
	that.element.style.backgroundImage = 'none';
	that.container.className = 'container_radius_bottom';
	that.element.appendChild(that.header);
	that.element.appendChild(that.container);
	that.insert_close_button();

	el_arrow_space = kite.browser.dom.eac('div', that.element, 'pop_up_arrow_space');
	el_arrow_container = kite.browser.dom.eac('div', el_arrow_space, 'pop_up_arrow_container');
	el_arrow = kite.browser.dom.ea('img', el_arrow_container);
	el_arrow.src = '/public/inlund/img/pop_up_arrow.png';

	that.action = function (el_target, target_position) {
		that.element.style.top = target_position.top + 'px';
		kite.browser.animation.Slide_up(that.element, {duration : 100, padding: 1, callback : function () {
			that.size();
		}});
	};

	return that;
};

kite.browser.ui.Drop_down = function () {
	var that = new kite.browser.ui.Window_core();

	that.close_on = 'click';
	that.container.className = 'container_radius_no_padding';
	that.element.appendChild(that.container);

	that.action = function (el_target, target_position) {
		that.element.style.top = target_position.top + el_target.offsetHeight + 'px';
		kite.browser.animation.Slide_down(that.element, {duration : 100, padding: 1, callback : function () {
			that.size();
		}});
	};

	return that;
};

kite.browser.ui.get_offset = function (element) {
	var left, top;

	left = element.offsetLeft;
	top = element.offsetTop;

	element = element.offsetParent;
	while (element) {
		left += element.offsetLeft;
		top += element.offsetTop;
		element = element.offsetParent;
	}

	return {left : left, top : top};
};

kite.browser.ui.set_opacity = function (element, value) {
	element.style.opacity = value;
	element.style.filter = 'alpha(opacity = ' + value * 100 + ')';
};

kite.browser.ui.cursor_position = function (event) {
	// Get cursor position with respect to the page.
	return {x: event.clientX + window.scrollX, y: event.clientY + window.scrollY};
};


kite.browser.ui.Move_resize_core = function (element, options) {
	this.options = {};

	// Default options
	this.drag = {
		element:					element,
		container:				element.parentNode,
		direction:				null,
		padding:					0,
		step_size:				1
	};

	this.change_options(options);
};

kite.browser.ui.Move_resize_core.prototype.drag_start = function (e, options) {
	var that, cursor, stop;

	e.preventDefault();

	that = this;
	that.drag_callback = options.drag_callback ? options.drag_callback : function () {};

	cursor = kite.browser.ui.cursor_position(e);

	if (this.drag.antagonist) {
		this.drag.start_width_antagonist = this.drag.antagonist.offsetWidth;
		this.drag.start_height_antagonist = this.drag.antagonist.offsetHeight;
	}

	this.drag.start_width = this.drag.element.offsetWidth;
	this.drag.start_height = this.drag.element.offsetHeight;
	this.drag.start_left = this.drag.element.offsetLeft;
	this.drag.start_top = this.drag.element.offsetTop;

	this.drag.max_offset_left = (this.options.max_offset_left - this.drag.padding) || -5000;
	this.drag.max_offset_right = (this.options.max_offset_right - this.drag.padding) || (this.drag.container ? this.drag.container.offsetWidth - this.drag.padding : 5000);
	this.drag.max_offset_top = (this.options.max_offset_top - this.drag.padding) || 0;
	this.drag.max_offset_bottom = (this.options.max_offset_bottom - this.drag.padding) || (this.drag.container ? this.drag.container.offsetHeight - this.drag.padding : 5000);

	this.drag.cursor_start_x = cursor.x;
	this.drag.cursor_start_y = cursor.y;

	stop = function (e) {
		document.removeEventListener("mousemove", that.go, false);
		document.removeEventListener("mouseup", stop, false);
		if (options.stop_callback) {
			options.stop_callback();
		}
	};

	document.addEventListener("mousemove", this.go, false);
	document.addEventListener("mouseup", stop, false);
};

kite.browser.ui.Move_resize_core.prototype.change_options = function (options) {
	var option;
	for (option in options) {
		if (options.hasOwnProperty(option)) {
			this.options[option] = options[option];
			this.drag[option] = options[option];
		}
	}
};

kite.browser.ui.Move = function (element, options) {
	var that;

	that = new kite.browser.ui.Move_resize_core(element, options);

	that.go = function (e) {
		var cursor, offset;

		cursor = kite.browser.ui.cursor_position(e);
		e.preventDefault();

		if (that.drag.direction !== 'vertical') {
			offset = that.drag.start_left + kite.browser.ui.cursor_position(e).x - that.drag.cursor_start_x;
			if (offset < that.drag.max_offset_left) {
				that.drag.element.style.left = that.drag.max_offset_left + "px";
			} else if (offset < that.drag.max_offset_right) {
				that.drag.element.style.left = offset + "px";
			} else if (offset > that.drag.max_offset_right || cursor.x > 0) {
				that.drag.element.style.left = that.drag.max_offset_right + "px";
			}
		}

		if (that.drag.direction !== 'horizontal') {
			offset = that.drag.start_top + kite.browser.ui.cursor_position(e).y - that.drag.cursor_start_y;
			if (offset < that.drag.max_offset_top) {
				that.drag.element.style.top = that.drag.max_offset_top + "px";
			} else if (offset < that.drag.max_offset_bottom) {
				that.drag.element.style.top = offset + "px";
			} else if (offset > that.drag.max_offset_bottom) {
				that.drag.element.style.top = that.drag.max_offset_bottom + "px";
			}
		}

		if (that.drag.move_callback) {
			that.drag.move_callback(e);
		}
	};
	return that;
};

kite.browser.ui.Resize = function (element, options) {
	var that;

	that = new kite.browser.ui.Move_resize_core(element, options);

	that.go = function (e) {
		var cursor, reverse, width, height;

		e.preventDefault();
		cursor = kite.browser.ui.cursor_position(e);
		reverse = 1;
		width = null;
		height = null;

		if (that.drag.reverse) {
			reverse = -1;
		}

		if (that.drag.direction !== 'vertical' && cursor.x + 15 <= document.documentElement.clientWidth && cursor.x > 0) {
			width = (that.drag.start_width + (cursor.x - that.drag.cursor_start_x) * reverse);
			that.drag.element.style.width = width + "px";
			if (that.drag.antagonist) {
				that.drag.antagonist.style.width = (that.drag.start_width_antagonist + (cursor.x - that.drag.cursor_start_x) * -1 * reverse) + "px";
			}
		}
		if (that.drag.direction !== 'horizontal' && cursor.y + 15 <= document.documentElement.clientHeight && cursor.y > 0) {
			height = (that.drag.start_height + (cursor.y - that.drag.cursor_start_y) * reverse);
			that.drag.element.style.height = height + "px";
			if (that.drag.antagonist) {
				that.drag.antagonist.style.height = (that.drag.start_height + (cursor.y - that.drag.cursor_start_y) * -1 * reverse) + "px";
			}
		}
		if (that.drag_callback) {
			that.drag_callback(e, width, height);
		}
	};
	return that;
};

"use strict";

kite.browser.animation = {};

kite.browser.animation.Core = function (options) {
	var option;

	// Default options
	this.options = {
		duration:	200,
		fps:			100,
		from:			0,
		to:				200,
		padding:	0
	};

	for (option in options) {
		if (options.hasOwnProperty(option)) {
			this.options[option] = options[option];
		}
	}

	if (this.options.element2) {
		this.options.element2.start_width = this.options.element2.start_width || this.options.element2.element.offsetWidth;
		this.options.element2.padding = this.options.element2.padding || 0;
	}

	this.start_on				= 0;
	this.finish_on			= this.start_on - this.options.duration;
	this.from_to_delta	= this.options.to - this.options.from;
	this.total_time			= this.finish_on - this.start_on;
	this.total_frames		= this.options.fps * (this.options.duration / 1000);
};

kite.browser.animation.Core.prototype.render = function () {
	var that, i, step;

	that = this;
	i = 1;

	step = function () {
		that.action(i);
		if (i < that.total_frames) {
			i += 1;
			setTimeout(step, 1000 / that.options.fps);
		} else {
			that.end();
			if (that.options.callback) {
				that.options.callback();
			}
		}
	};
	setTimeout(step, 1000 / this.options.fps);
};

kite.browser.animation.Hide_up = function (element, options) {
	var that = new kite.browser.animation.Core(options);
	that.init = function () {
		that.target_height = that.options.target_height || element.offsetHeight;
		that.target_top = that.options.target_top || element.offsetTop - that.target_height;
		that.start_top = element.offsetTop;
	};
	that.end = function () { // Things to do at the end of the animation
		element.style.top = that.target_top + 'px';
	};
	that.action = function (frame) { // Happens at each step
		var step_size = Math.round((frame / that.total_frames) * that.target_height);
		element.style.top = that.start_top - step_size + 'px';
	};
	that.init();
	that.render();
};

kite.browser.animation.Slide_up = function (element, options) {
	var that = new kite.browser.animation.Core(options);
	that.init = function () {
		that.target_height = that.options.target_height || element.offsetHeight;
		that.target_top = that.options.target_top || element.offsetTop - that.target_height;
		that.start_top = element.offsetTop;
		element.style.height = '0px';
		element.style.overflow = 'hidden';
	};
	that.end = function () { // Things to do at the end of the animation
		element.style.top = that.target_top + 'px';
		element.style.overflow = 'visible';
		element.style.height = 'auto';
	};
	that.action = function (frame) { // Happens at each step
		var step_size = Math.round((frame / that.total_frames) * that.target_height);
		if (element.offsetHeight < that.target_height) {
			element.style.height = (step_size - (that.options.padding * 2)) + 'px'; // top and bottom padding is removed
		}
		element.style.top = that.start_top - step_size + 'px';
	};
	that.init();
	that.render();
};

kite.browser.animation.Slide_down = function (element, options) {
	var that = new kite.browser.animation.Core(options);
	that.init = function () {
		that.target_height = that.options.target_height || element.offsetHeight;
		that.child = element.firstChild;
		that.target_top = 0;
		that.start_child_top = -1 * that.target_height;
		that.child.style.position = 'relative';
		that.child.style.top = that.start_child_top + 'px';
		element.style.height = '0px';
		element.style.overflow = 'hidden';
	};
	that.top = function (element) {
		if (window.innerHeight < element.offsetTop + element.offsetHeight) {
			element.style.top = (window.innerHeight - element.offsetHeight) + 'px';
		}
	};
	that.end = function () { // Things to do at the end of the animation
		that.child.style.top = that.target_top + 'px';
		element.style.overflow = 'visible';
		element.style.height = 'auto';
		that.top(element);
	};
	that.action = function (frame) { // Happens at each step
		var step_size, height;

		step_size = Math.round((frame / that.total_frames) * that.target_height);

		if (element.offsetHeight < that.target_height) {
			height = (step_size - (that.options.padding * 2));
			element.style.height = height + 'px'; // top and bottom padding is removed
			that.top(element);
			that.child.style.top = (that.start_child_top + step_size - that.options.padding) + 'px';
		}
	};
	that.init();
	that.render();
};

kite.browser.animation.Slide_in_right = function (element, options) {
	var that = new kite.browser.animation.Core(options);
	that.init = function () {
		that.start_width = that.options.start_width || element.offsetWidth;
		that.target_width = that.options.target_width || 0;
	};
	that.end = function () { // Things to do at the end of the animation
		element.style.width = that.target_width + 'px';
	};
	that.action = function (frame) { // Happens at each step
		var step_size = Math.round((frame / that.total_frames) * that.start_width);
		if (element.offsetWidth > that.target_width) {
			element.style.width = (that.start_width - step_size - (that.options.padding * 2)) + 'px'; // top and bottom padding is removed
			if (that.options.element2) {
				that.options.element2.element.style.width = (that.options.element2.start_width + step_size - (that.options.element2.padding * 2)) + 'px';
			}
		}
	};
	that.init();
	that.render();
};

kite.browser.animation.Slide_out_left = function (element, options) {
	var that = new kite.browser.animation.Core(options);
	that.init = function () {
		that.start_width = that.options.start_width || element.offsetWidth;
		that.target_width = that.options.target_width || 0;
	};
	that.end = function () { // Things to do at the end of the animation
		element.style.width = that.target_width + 'px';
	};
	that.action = function (frame) { // Happens at each step
		var step_size = Math.round((frame / that.total_frames) * that.target_width);
		if (element.offsetWidth < that.target_width) {
			element.style.width = (step_size - (that.options.padding * 2)) + 'px'; // top and bottom padding is removed
			if (that.options.element2) {
				that.options.element2.element.style.width = (that.options.element2.start_width - step_size - (that.options.element2.padding * 2)) + 'px';
			}
		}
	};
	that.init();
	that.render();
};

kite.browser.animation.Resize = function (element, options) {
	var that = new kite.browser.animation.Core(options);
	that.init = function () {
		that.target_height = that.options.target_height >= 0 ? that.options.target_height : element.offsetHeight;
		that.target_width = that.options.target_width >= 0 ? that.options.target_width : element.offsetWidth;
		that.start_height = that.options.start_height >= 0 ? that.options.start_height : element.offsetHeight;
		that.start_width = that.options.start_width >= 0 ? that.options.start_width : element.offsetWidth;
	};
	that.end = function () { // Things to do at the end of the animation
		if (options.target_height >= 0) {
			element.style.height = that.target_height + 'px';
		}
		if (options.target_width >= 0) {
			element.style.width = that.target_width + 'px';
		}
	};
	that.action = function (frame) { // Happens at each step
		var step_size = frame / that.total_frames;
		if (options.target_height >= 0 && that.start_height !== that.target_height) {
			element.style.height = Math.round(that.start_height + step_size * (that.target_height - that.start_height)) + 'px';
		}
		if (options.target_width >= 0 && that.start_width !== that.target_width) {
			element.style.width = Math.round(that.start_width + step_size * (that.target_width - that.start_width)) + 'px';
		}
	};
	that.init();
	that.render();
};

kite.browser.animation.Fade_out = function (element, options) { // time in milliseconds
	var that = new kite.browser.animation.Core(options);
	that.init = function () {
		that.start = 1;
		that.target = 0;
	};
	that.end = function () {
		element.style.opacity = that.target;
//		element.style.display = 'none';
	};
	that.action = function (frame) {
		element.style.opacity = that.start - (frame / that.total_frames);
	};
	that.init();
	that.render();
};

kite.browser.animation.Fade_in = function (element, options) { // time in milliseconds
	var that = new kite.browser.animation.Core(options);
	that.init = function () {
		that.start = 0;
		that.target = 1;
		element.style.display = 'block';
	};
	that.end = function () {
		element.style.opacity = that.target;
	};
	that.action = function (frame) {
		element.style.opacity = (frame / that.total_frames) * that.target;
	};
	that.init();
	that.render();
};

kite.browser.animation.Highlight = function (element, options) { // time in milliseconds
	var that, val;
	that = new kite.browser.animation.Core(options);
	that.init = function () {
		that.start_rgb = options.start_rgb;
		that.target_rgb = {r: options.target_rgb.r - options.start_rgb.r, g: options.target_rgb.g - options.start_rgb.g, b: options.target_rgb.b - options.start_rgb.b};
	};
	that.end = function () {
		element.style.backgroundColor = '';
	};
	that.action = function (frame) {
		val = frame / that.total_frames;
		element.style.backgroundColor = 'rgb(' + Math.ceil(val * that.target_rgb.r + that.start_rgb.r) + ',' + Math.ceil(val * that.target_rgb.g + that.start_rgb.g) + ',' + Math.ceil(val * that.target_rgb.b + that.start_rgb.b) + ')';
	};
	that.init();
	that.render();
};

kite.browser.animation.Scroll = function (element, options) { // time in milliseconds
	var that = new kite.browser.animation.Core(options);
	that.init = function () {
		that.start = element.scrollLeft;
	};
	that.end = function () {
		element.scrollLeft = options.to;
	};
	that.action = function (frame) {
		element.scrollLeft = that.start + ((options.to - that.start) / that.total_frames) * frame;
	};
	that.init();
	that.render();
};

kite.browser.animation.shake = function (element, callback) {
	var start_position, step, distance, factor, shake;

	start_position = element.offsetLeft;
	step = 5;
	distance = 0;
	factor = 1;

	shake = setInterval(function () {
		element.style.left =	element.offsetLeft + step * factor + 'px';
		distance = distance + step * factor;
		if (distance >= 20 || distance <= -20) {
			factor = factor * -1;
		}
	}, 10);

	setTimeout(function () {
		clearInterval(shake);
		element.style.left = start_position + 'px';
		if (callback) {
			callback();
		}
	}, 400);
};


nbe.browser.icon.network = function (parent) {
	var off_text, el_icon, el_network, el_bolt;

	off_text = 'You offline';

	el_icon = kite.browser.dom.ea('div', parent);
	el_icon.title = off_text;
	el_network = kite.browser.dom.svg(-8, -8, 48, 48, 'circle_button', el_icon);
	el_bolt = kite.browser.dom.ns('polygon', el_network, ['points', '32,0 8,16 14,20 0,32 24,20 18,16']);

	return {on : function () {
		el_bolt.setAttribute('fill', 'lightgreen');
		el_icon.title = 'You are online';
	}, off : function () {
		el_bolt.setAttribute('fill', 'red');
		el_icon.title = off_text;
	}};
};

nbe.browser.icon.saved = function (parent) {
	var on_text, el_icon, el_saved, el_cloud, el_arrow;

	on_text = 'The document is saved';

	el_icon = kite.browser.dom.ea('div', parent);
	el_icon.title = on_text;
	el_saved = kite.browser.dom.svg(-8, -8, 48, 48, 'circle_button', el_icon);
	el_cloud = kite.browser.dom.ns('path', el_saved, ['d', 'M24,4c-0.375,0-0.738,0.062-1.102,0.109C21.504,1.648,18.926,0,16,0c-2.988,0-5.568,1.664-6.941,4.102C8.707,4.055,8.357,4,8,4c-4.412,0-8,3.586-8,8s3.588,8,8,8h16c4.414,0,8-3.586,8-8S28.414,4,24,4z M24,16H8c-2.205,0-4-1.797-4-4c0-2.195,1.943-3.883,4.004-3.945C8.012,9,8.176,9.922,8.504,10.797l3.746-1.398C12.084,8.953,12,8.484,12,8c0-2.203,1.795-4,4-4c1.295,0,2.463,0.641,3.201,1.641C17.27,7.102,16,9.395,16,12h4c0-2.203,1.797-4,4-4s4,1.797,4,4S26.203,16,24,16z']);
	el_arrow = kite.browser.dom.ns('polygon', el_saved, ['points', '18.002,26 22,26 16.004,20 10.002,26 14.002,26 14.002,32 18.002,32']);

	return {on : function () {
		el_cloud.setAttribute('fill', 'lightgreen');
		el_arrow.setAttribute('fill', 'lightgreen');
		el_icon.title = on_text;
	}, off : function () {
		el_cloud.setAttribute('fill', 'red');
		el_arrow.setAttribute('fill', 'red');
		el_icon.title = 'The document is not saved';
	}};
};

nbe.browser.icon.exporticon = function (parent) {
	var el_icon, el_export, el_rect, el_arrow;

	el_icon = kite.browser.dom.ea('div', parent);
	el_icon.title = 'Export';

	el_export = kite.browser.dom.svg(-16, -11, 56, 56, 'circle_button', el_icon);

	el_rect = kite.browser.dom.ns('rect', el_export, ['y', '27.43']);
	el_rect.style.fill = '#FFFFFF';
	el_rect.setAttribute('width', 24);
	el_rect.setAttribute('height', 4.57);

	el_arrow = kite.browser.dom.ns('polygon', el_export, ['points', '16,18.285 16,0 8,0 8,18.285 4,18.285 12.012,27.43 20,18.285']);
	el_arrow.style.fill = '#FFFFFF';

	return el_icon;
};

nbe.inputs.color_menu = function (trigger, default_color, default_label, colors, init) {
	var is_open, el_panel, element, value, swatches, create_swatch, el_default, rgb_input, el_custom, el_custom_swatch, el_r, el_g, el_b, el_default_label, i, remove, remove_handler, switch_swatch;

	is_open = false;

	el_panel = document.body;

	element = kite.browser.dom.ec('div', 'wu-menu wu-color_menu');
	element.addEventListener('click', function (e) {
		var color;

		color = e.target.getAttribute('data-color');

		if (color) {
			switch_swatch(color);
		}
	}, false);

	value = init;
	swatches = {};

	create_swatch = function (color, parent) {
		var el_swatch;

		el_swatch = kite.browser.dom.eac('div', parent, 'wu-color_swatch');
		el_swatch.style.backgroundColor = color;
		el_swatch.setAttribute('data-color', color);

		return el_swatch;
	};

	el_default = kite.browser.dom.eac('div', element, 'wu-color_default');

	rgb_input = function (e) {
		var new_value;

		if (el_r.value !== '' && el_g.value !== '' && el_b.value !== '') {
			new_value = 'rgb(' + el_r.value + ', ' + el_g.value + ', ' + el_b.value + ')';

			el_custom_swatch.style.backgroundColor = new_value;
			switch_swatch(new_value);
		} else {
			switch_swatch(init);
		}
	};

	el_custom = kite.browser.dom.eac('div', element, 'wu-color_custom');
	el_custom_swatch = kite.browser.dom.eac('div', el_custom, 'wu-color_swatch');
	el_custom_swatch.addEventListener('click', function (e) {
		rgb_input(e);
	}, false);

	kite.browser.dom.ea('span', el_custom).textContent = 'R:';
	el_r = kite.browser.dom.ea('input', el_custom);
	el_r.addEventListener('keyup', rgb_input, false);

	kite.browser.dom.ea('span', el_custom).textContent = 'G:';
	el_g = kite.browser.dom.ea('input', el_custom);
	el_g.addEventListener('keyup', rgb_input, false);

	kite.browser.dom.ea('span', el_custom).textContent = 'B:';
	el_b = kite.browser.dom.ea('input', el_custom);
	el_b.addEventListener('keyup', rgb_input, false);

	swatches[default_color] = create_swatch(default_color, el_default);

	el_default_label = kite.browser.dom.ea('span', el_default);
	el_default_label.textContent = default_label;
	el_default_label.setAttribute('data-color', default_color);

	for (i = 0; i < colors.length; i++) {
		swatches[colors[i]] = create_swatch(colors[i], element);
	}

	remove = function () {
		is_open = false;
		el_panel.removeChild(element);
		document.body.removeEventListener('click', remove_handler, false);
		trigger(value);
	};

	remove_handler = function (e) {
		if (e.target !== el_r && e.target !== el_g && e.target !== el_b) {
			remove();
		}
	};

	switch_swatch = function (new_value) {
		if (swatches[value]) {
			swatches[value].classList.remove('wu-selected');
		}

		el_custom_swatch.classList.remove('wu-selected');
		el_custom_swatch.style.backgroundColor = 'transparent';

		if (swatches[new_value]) {
			swatches[new_value].classList.add('wu-selected');
		} else {
			el_custom_swatch.classList.add('wu-selected');
			el_custom_swatch.style.backgroundColor = new_value;
		}

		value = new_value;
	};

	return {display : function (parent, offset_element, new_value) {
		var rgb, offset;

		is_open = true;

		el_panel.appendChild(element);

		offset = kite.browser.ui.get_offset(offset_element);
		element.style.left = (offset.left - (element.offsetWidth / 2) + (offset_element.offsetWidth / 2)) + 'px';
		element.style.top = offset.top + offset_element.offsetHeight + 'px';

		document.body.addEventListener('click', remove_handler, false);

		switch_swatch(new_value);

		if (swatches[new_value]) {
			if (el_r.value !== '' && el_g.value !== '' && el_b.value !== '') {
				el_custom_swatch.style.backgroundColor = 'rgb(' + el_r.value + ', ' + el_g.value + ', ' + el_b.value + ')';
			}
		} else {
			rgb = new_value.match(/^rgb\((\d+), (\d+), (\d+)\)$/);
			el_r.value = rgb[1];
			el_g.value = rgb[2];
			el_b.value = rgb[3];
		}
	}, remove : remove, is_open : function () {
		return is_open;
	}};
};

nbe.inputs.input = function (type, trigger) {
	var triggers, add_trigger, remove_trigger;

	triggers = trigger ? [trigger] : [];

	add_trigger = function (trigger) {
		var i, add;

		add = true;

		for (i = 0; i < triggers.length; i++) {
			if (triggers[i] === trigger) {
				add = false;
			}
		}

		if (add) {
			triggers.push(trigger);
		}
	};

	remove_trigger = function (trigger) {
		var i;

		for (i = 0; i < triggers.length; i++) {
			if (triggers[i] === trigger) {
				triggers.splice(i, 1);
			}
		}
	};

	return {editors : triggers, add_trigger : add_trigger, remove_trigger : remove_trigger, trigger : function (value) {
		var i;

		for (i = 0; i < triggers.length; i++) {
			triggers[i](type, value);
		}
	}, get_triggers : function () {
		return triggers;
	}};

};


nbe.inputs.button = function (type, title, parent, trigger, init) {
	var input, value, element, set_value;

	input = nbe.inputs.input(type, trigger);

	value = null;
	element = kite.browser.dom.eac('button', parent, 'wu-icon wu-icon-' + type + ' off');
	element.title = title;

	set_value = function (new_value) {
		if (value !== new_value) {
			value = new_value;
			element.className = 'wu-icon wu-icon-' + type + ' ' + value;
		}
	};

	set_value(init);

	element.addEventListener('click', function () {
		input.trigger(value === 'off' ? 'on' : 'off');
	});

	input.element = element;
	input.set_value = set_value;

	return input;
};


nbe.inputs.bold = function (trigger, title, parent, init) {
	var button;

	button = nbe.inputs.button('bold', title, parent, trigger, init);
	button.element.textContent = 'B';

	return button;
};


nbe.inputs.italic = function (trigger, title, parent, init) {
	var button;

	button = nbe.inputs.button('italic', title, parent, trigger, init);
	button.element.textContent = 'I';

	return button;
};


nbe.inputs.underline = function (trigger, title, parent, init) {
	var button;

	button = nbe.inputs.button('underline', title, parent, trigger, init);
	button.element.textContent = 'U';

	return button;
};


nbe.inputs.strikethrough = function (trigger, title, parent, init) {
	var button;

	button = nbe.inputs.button('strikethrough', title, parent, trigger, init);
	button.element.textContent = 'S';

	return button;
};


nbe.inputs.color = function (trigger, title, parent, init) {
	var button, value, element, color_menu, set_value;

	button = nbe.inputs.input('color', trigger);

	value = null;
	element = kite.browser.dom.eac('button', parent, 'wu-icon off');
	element.title = title;
	element.textContent = 'A';

	color_menu = nbe.inputs.color_menu(function (color) {
		button.trigger(color);
	}, 'rgb(0, 0, 0)', 'Black', [
		'rgb(255, 200, 200)', 'rgb(255, 200, 75)', 'rgb(255, 255, 200)', 'rgb(200, 255, 0)', 'rgb(200, 255, 200)', 'rgb(150, 255, 225)', 'rgb(200, 255, 255)', 'rgb(135, 240, 255)', 'rgb(100, 175, 255)', 'rgb(235, 120, 255)', 'rgb(255, 100, 200)', 'rgb(224,224,224)',
		'rgb(255, 150, 150)', 'rgb(255, 175, 50)', 'rgb(255, 255, 150)', 'rgb(175, 255, 0)', 'rgb(150, 255, 150)', 'rgb(100, 255, 200)', 'rgb(150, 255, 255)', 'rgb(80, 235, 255)', 'rgb(0, 150, 255)', 'rgb(200, 80, 255)', 'rgb(237, 0, 175)', 'rgb(192,192,192)',
		'rgb(255, 100, 100)', 'rgb(255, 150, 25)', 'rgb(255, 255, 100)', 'rgb(150, 255, 0)', 'rgb(100, 255, 100)', 'rgb(50, 255, 175)', 'rgb(100, 255, 255)', 'rgb(50, 220, 255)', 'rgb(0, 100, 255)', 'rgb(175, 40, 255)', 'rgb(218, 0, 150)', 'rgb(160,160,160)',
		'rgb(255, 0, 0)', 'rgb(255, 125, 0)', 'rgb(255, 255, 0)', 'rgb(125, 255, 0)', 'rgb(0, 255, 0)', 'rgb(0, 255, 150)', 'rgb(0, 255, 255)', 'rgb(0, 200, 255)', 'rgb(0, 0, 255)', 'rgb(150, 0, 255)', 'rgb(200, 0, 125)', 'rgb(128,128,128)',
		'rgb(200 ,0, 0)', 'rgb(200, 100, 0)', 'rgb(200, 200, 0)', 'rgb(100, 200, 0)', 'rgb(0, 200, 0)', 'rgb(0, 200, 125)', 'rgb(0, 200, 200)', 'rgb(0, 170, 225)', 'rgb(0, 0, 200)', 'rgb(125, 0, 200)', 'rgb(170, 0, 105)', 'rgb(96,96,96)',
		'rgb(150, 0, 0)', 'rgb(150, 75, 0)', 'rgb(150, 150, 0)', 'rgb(75, 150, 0)', 'rgb(0, 150, 0)', 'rgb(0, 150, 100)', 'rgb(0, 150, 150)', 'rgb(0, 140, 195)', 'rgb(0, 0, 150)', 'rgb(100, 0, 150)', 'rgb(140, 0, 85)', 'rgb(64,64,64)',
		'rgb(100, 0, 0)', 'rgb(100, 50, 0)', 'rgb(100, 100, 0)', 'rgb(50, 100, 0)', 'rgb(0, 100, 0)', 'rgb(0, 100, 75)', 'rgb(0, 100, 100)', 'rgb(0, 110, 165)', 'rgb(0, 0, 100)', 'rgb(75, 0, 100)', 'rgb(110, 0, 65)', 'rgb(32,32,32)'
	], init);

	set_value = function (new_value) {
		if (value !== new_value) {
			value = new_value;
			element.style.color = value;
		}
	};

	set_value(init);

	element.addEventListener('click', function (e) {
		e.stopPropagation();
		if (color_menu.is_open()) {
			color_menu.remove();
		} else {
			color_menu.display(parent, element, value);
		}
	}, false);

	button.element = element;
	button.set_value = set_value;

	return button;
};


nbe.inputs.background_color = function (trigger, title, parent, init) {
	var button, value, element, el_symbol, color_menu, set_value;

	button = nbe.inputs.input('background_color', trigger);

	value = null;
	element = kite.browser.dom.eac('button', parent, 'wu-icon wu-icon-background_color off');
	element.title = title;
	el_symbol = kite.browser.dom.ea('div', element);
	el_symbol.textContent = 'A';

	color_menu = nbe.inputs.color_menu(function (color) {
		button.trigger(color);
	}, 'transparent', 'None', [
		'rgb(255, 200, 200)', 'rgb(255, 200, 75)', 'rgb(255, 255, 200)', 'rgb(200, 255, 0)', 'rgb(200, 255, 200)', 'rgb(150, 255, 225)', 'rgb(200, 255, 255)', 'rgb(135, 240, 255)', 'rgb(100, 175, 255)', 'rgb(235, 120, 255)', 'rgb(255, 100, 200)', 'rgb(224,224,224)',
		'rgb(255, 150, 150)', 'rgb(255, 175, 50)', 'rgb(255, 255, 150)', 'rgb(175, 255, 0)', 'rgb(150, 255, 150)', 'rgb(100, 255, 200)', 'rgb(150, 255, 255)', 'rgb(80, 235, 255)', 'rgb(0, 150, 255)', 'rgb(200, 80, 255)', 'rgb(237, 0, 175)', 'rgb(192,192,192)',
		'rgb(255, 100, 100)', 'rgb(255, 150, 25)', 'rgb(255, 255, 100)', 'rgb(150, 255, 0)', 'rgb(100, 255, 100)', 'rgb(50, 255, 175)', 'rgb(100, 255, 255)', 'rgb(50, 220, 255)', 'rgb(0, 100, 255)', 'rgb(175, 40, 255)', 'rgb(218, 0, 150)', 'rgb(160,160,160)',
		'rgb(255, 0, 0)', 'rgb(255, 125, 0)', 'rgb(255, 255, 0)', 'rgb(125, 255, 0)', 'rgb(0, 255, 0)', 'rgb(0, 255, 150)', 'rgb(0, 255, 255)', 'rgb(0, 200, 255)', 'rgb(0, 0, 255)', 'rgb(150, 0, 255)', 'rgb(200, 0, 125)', 'rgb(128,128,128)',
		'rgb(200 ,0, 0)', 'rgb(200, 100, 0)', 'rgb(200, 200, 0)', 'rgb(100, 200, 0)', 'rgb(0, 200, 0)', 'rgb(0, 200, 125)', 'rgb(0, 200, 200)', 'rgb(0, 170, 225)', 'rgb(0, 0, 200)', 'rgb(125, 0, 200)', 'rgb(170, 0, 105)', 'rgb(96,96,96)',
		'rgb(150, 0, 0)', 'rgb(150, 75, 0)', 'rgb(150, 150, 0)', 'rgb(75, 150, 0)', 'rgb(0, 150, 0)', 'rgb(0, 150, 100)', 'rgb(0, 150, 150)', 'rgb(0, 140, 195)', 'rgb(0, 0, 150)', 'rgb(100, 0, 150)', 'rgb(140, 0, 85)', 'rgb(64,64,64)',
		'rgb(100, 0, 0)', 'rgb(100, 50, 0)', 'rgb(100, 100, 0)', 'rgb(50, 100, 0)', 'rgb(0, 100, 0)', 'rgb(0, 100, 75)', 'rgb(0, 100, 100)', 'rgb(0, 110, 165)', 'rgb(0, 0, 100)', 'rgb(75, 0, 100)', 'rgb(110, 0, 65)', 'rgb(32,32,32)'
	], init);

	set_value = function (new_value) {
		if (value !== new_value) {
			value = new_value;
			el_symbol.style.backgroundColor = value;
		}
	};

	set_value(init);

	element.addEventListener('click', function (e) {
		e.stopPropagation();
		if (color_menu.is_open()) {
			color_menu.remove();
		} else {
			color_menu.display(parent, element, value);
		}

	}, false);

	button.element = element;
	button.set_value = set_value;

	return button;
};


nbe.inputs.vertical_align = function (trigger, parent, init) {
	var el_container, input, button_trigger, sup, sub;

	el_container = kite.browser.dom.ea('div', parent);
	input = nbe.inputs.input('vertical_align', trigger);

	button_trigger = function (type, value) {
		if (value === 'on') {
			input.trigger(type);
		} else {
			input.trigger('baseline');
		}
	};

	sup = nbe.inputs.button('super', 'Superscript', el_container, button_trigger, 'off');
	sup.element.innerHTML = 'A<span>2</span>';
	sub = nbe.inputs.button('sub', 'Subscript', el_container, button_trigger, 'off');
	sub.element.innerHTML = 'A<span>2</span>';

	input.element = el_container;
	input.set_value = function (value) {
		if (value === 'super') {
			sup.set_value('on');
			sub.set_value('off');
		} else if (value === 'sub') {
			sub.set_value('on');
			sup.set_value('off');
		} else {
			sup.set_value('off');
			sub.set_value('off');
		}
	};

	input.set_value(init);

	return input;
};


nbe.inputs.left_margin = function (trigger, parent, init) {
	var current_value, el_container, input, decrease, increase;

	current_value = ['off', 'on'];

	el_container = kite.browser.dom.ea('div', parent);
	input = nbe.inputs.input('left_margin', trigger);

	decrease = nbe.inputs.button('decrease_indent', 'Decrease indentation', parent, function () {
		if (current_value[0] === 'on') {
			input.trigger('decrement');
		}
	}, 'off');
	decrease.element.textContent = '<';
	increase = nbe.inputs.button('increase_indent', 'Increase indentation', parent, function () {
		if (current_value[1] === 'on') {
			input.trigger('increment');
		}
	}, 'off');
	increase.element.textContent = '>';

	input.element = el_container;
	input.set_value = function (value) {
		current_value = value.split(':');
		decrease.set_value(current_value[0]);
		increase.set_value(current_value[1]);
	};

	input.set_value(init);

	return input;
};


nbe.inputs.undo = function (trigger, parent) {
	var el_container, input, undo, redo;

	el_container = kite.browser.dom.ea('div', parent);
	input = nbe.inputs.input('undo', trigger);

	undo = nbe.inputs.button('undo', 'Undo', el_container, function () {
		input.trigger('undo');
	}, 'off');
	kite.browser.dom.ea('img', undo.element).src = '/img/undo.svg';
	redo = nbe.inputs.button('redo', 'Redo', el_container, function () {
		input.trigger('redo');
	}, 'off');
	kite.browser.dom.ea('img', redo.element).src = '/img/redo.svg';

	input.element = el_container;
	input.set_value = function (value) {
		undo.set_value(value.undo ? 'on' : 'off');
		redo.set_value(value.redo ? 'on' : 'off');
	};

	return input;
};


nbe.inputs.drop_down = function (type, title, menu_content, button_content, parent, trigger, init, display_input) {
	var input, value, el_panel, element, el_input, input_handler, close, el_menu, options, key, set_value;

	input = nbe.inputs.input(type, trigger);

	value = null;

	el_panel = document.body;

	element = kite.browser.dom.eac('div', parent, 'wu-icon wu-drop-down wu-icon-' + type);
	element.title = title;
	element.addEventListener('click', function (e) {
		var offset;

		if (!el_menu.parentNode && e.target !== el_input) {
			offset = kite.browser.ui.get_offset(element);
			el_menu.style.left = offset.left + 1 + 'px';
			el_menu.style.top = offset.top + element.offsetHeight + 'px';
			el_panel.appendChild(el_menu);
			close = false;
			setTimeout(function () {
				close = true;
			}, 0);
		}
	}, true);

	el_input = document.createElement('input');
	if (display_input) {
		element.appendChild(el_input);
		el_input.type = 'text';
		input_handler = function (e) {
			var new_value = el_input.value.replace(/\s/g, '');

			if (isNaN(new_value)) {
				alert('Please specify a number.');
				set_value(value);
			} else {
				set_value(new_value + 'px');
				input.trigger(value);
			}
		};
		el_input.addEventListener('blur', input_handler, false);
		el_input.addEventListener('keyup', function (e) {
			if (e.keyCode === 13) {
				input_handler(e);
			}
		}, false);
	}

	document.body.addEventListener('click', function (e) {
		if (el_menu.parentNode && close) {
			el_panel.removeChild(el_menu);
		}
	}, false);

	el_menu = kite.browser.dom.ec('div', 'wu-menu drop_down_menu');
	el_menu.addEventListener('click', function (e) {
		var value;

		value = e.target.getAttribute('data-option') ? e.target.getAttribute('data-option') : e.target.parentNode.getAttribute('data-option');
		input.trigger(value);

		if (el_menu.parentNode) {
			el_panel.removeChild(el_menu);
		}
	}, false);

	options = {};

	for (key in menu_content) {
		if (menu_content.hasOwnProperty(key)) {
			options[key] = kite.browser.dom.eac('div', el_menu, 'wu-menu-row');
			options[key].setAttribute('data-option', key);
			options[key].innerHTML = menu_content[key];
		}
	}

	set_value = function (new_value) {
		if (value && value in options) {
			options[value].className = 'wu-menu-row';
		}
		value = new_value;
		if (value in options) {
			options[value].className = 'wu-menu-row wu-selected';
		}
		if (display_input) {
			el_input.value = value.replace('px', '');
		} else {
			element.innerHTML = button_content[value] ? button_content[value] : (menu_content[value] ? menu_content[value].replace(' (default)', '') : value);
		}
	};

	set_value(init);

	input.element = element;
	input.set_value = set_value;

	return input;
};


nbe.inputs.heading = function (trigger, title, menu_content, button_content, parent, init) {
	var drop_down;

	drop_down = nbe.inputs.drop_down('heading', title, menu_content, button_content, parent, trigger, init, false);

	return drop_down;
};


nbe.inputs.font_family = function (trigger, title, content, parent, init) {
	var drop_down;

	drop_down = nbe.inputs.drop_down('font_family', title, content, {}, parent, trigger, init, false);

	return drop_down;
};


nbe.inputs.font_size = function (trigger, title, content, parent, init) {
	var drop_down;

	drop_down = nbe.inputs.drop_down('font_size', title, content, {}, parent, trigger, init, true);

	return drop_down;
};


nbe.inputs.text_align = function (trigger, title, content, parent, init) {
	var drop_down;

	drop_down = nbe.inputs.drop_down('text_align', title, content, {}, parent, trigger, init, false);

	return drop_down;
};


nbe.inputs.line_spacing = function (trigger, title, content, parent, init) {
	var drop_down;

	drop_down = nbe.inputs.drop_down('line_spacing', title, content, {}, parent, trigger, init, false);

	return drop_down;
};


nbe.inputs.list = function (trigger, title, content, parent, init) {
	var drop_down;

	drop_down = nbe.inputs.drop_down('list', title, content, {}, parent, trigger, init, false);

	return drop_down;
};


nbe.inputs.special_characters = function (trigger, title, parent) {
	var button, element, drop_down, el_window, el_menu, sets, el_characters, char_interval, content, i, el_option, j, el_char, el_input, el_buttons, el_insert, el_cancel;

	button = nbe.inputs.input('text', trigger);

	element = kite.browser.dom.eac('button', parent, 'wu-icon wu-icon-special_characters off');
	element.title = title;
	//element.textContent = 'Sp. C.';

	drop_down = new kite.browser.ui.Window();
	drop_down.set_title('Special Characters');

	element.addEventListener('click', function (e) {
		e.stopPropagation();
		if (drop_down.is_open) {
			drop_down.close();
		} else {
			drop_down.open();
		}
	}, false);

	el_window = kite.browser.dom.ec('div', 'wu-special_characters');
	kite.browser.dom.ea('div', el_window).textContent = 'Please choose character sets: ';
	el_menu = kite.browser.dom.ea('select', el_window);
	sets = [];
	el_characters = kite.browser.dom.ea('div', el_window);

	char_interval = function (lower, upper) {
		var chars, i;

		chars = [];
		for (i = lower; i <= upper; i++) {
			chars.push(String.fromCharCode(i));
		}

		return chars;
	};

	content = [{
		name : 'latin extended',
		characters : char_interval(192, 687)
	}, {
		name : 'greek and coptic',
		characters : char_interval(880, 1023)
	}, {
		name : 'mathematical operators',
		characters : char_interval(8704, 8959)
	}, {
		name : 'arrows',
		characters : char_interval(8592, 8703)
	}, {
		name : 'currency',
		characters : char_interval(8352, 8399)
	}];

	for (i = 0; i < content.length; i = i + 1) {
		sets[i] = kite.browser.dom.ec('div', 'wu-character_set');
		el_option = kite.browser.dom.ea('option', el_menu);
		el_option.textContent = content[i].name;
		el_option.value = i;
		for (j = 0; j < content[i].characters.length; j = j + 1) {
			el_char = kite.browser.dom.ea('div', sets[i]);
			el_char.textContent = content[i].characters[j];
			if (j % 11 === 0) {
				el_char.style.clear = 'left';
			}
		}
	}
	// Default character set:
	el_characters.appendChild(sets[0]);

	el_menu.addEventListener('change', function (e) {
		el_characters.removeChild(el_characters.firstChild);
		el_characters.appendChild(sets[e.target.value]);
	}, false);

	kite.browser.dom.ea('div', el_window).textContent = 'Characters to insert:';
	el_input = kite.browser.dom.ea('input', el_window);

	el_buttons = kite.browser.dom.eac('div', el_window, 'wu-special_character_buttons');
	el_insert = kite.browser.dom.eac('button', el_buttons, 'button');
	el_insert.textContent = 'Insert characters';
	el_cancel = kite.browser.dom.eac('button', el_buttons, 'button');
	el_cancel.textContent = 'Cancel';

	drop_down.set_content(el_window);

	el_window.addEventListener('click', function (e) {
		if (el_insert === e.target) {
			button.trigger(el_input.value);
			el_input.value = '';
			drop_down.close();
		} else if (el_cancel === e.target) {
			drop_down.close();
		} else if (e.target.parentNode.className === 'wu-character_set') {
			el_input.value += e.target.textContent;
		}
	}, false);

	button.element = element;
	return button;
};


nbe.inputs.insert_link = function (trigger, title, parent) {
	var button, element, drop_down, insertion, el_window, el_link_text_container, el_text_message, el_link_text, el_link_url_container, el_url_message, el_link_url, el_buttons, el_insert, el_cancel;

	button = nbe.inputs.input('link', trigger);

	element = kite.browser.dom.eac('button', parent, 'wu-icon wu-icon-insert_link off');
	element.title = title;
	//element.textContent = '+ Link';

	drop_down = new kite.browser.ui.Window();
	drop_down.set_title('Insert link');

	element.addEventListener('click', function (e) {
		e.stopPropagation();

		if (drop_down.is_open) {
			drop_down.close();
		} else {
			insertion = false;//nbe.paste.link_text(button.get_triggers()[0]);
			if (!insertion) {
				el_window.insertBefore(el_link_text_container, el_link_url_container);
			} else {
				if (el_link_text_container.parentNode) {
					el_window.removeChild(el_link_text_container);
				}
			}
			el_text_message.textContent = '';
			el_url_message.textContent = '';
			drop_down.open();
		}
	}, false);

	el_window = kite.browser.dom.ec('div', 'wu-special_characters');

	el_link_text_container = document.createElement('div');
	kite.browser.dom.ea('span', el_link_text_container).textContent = 'Link text: ';
	el_text_message = kite.browser.dom.eac('span', el_link_text_container, 'message_failure');
	kite.browser.dom.ea('br', el_link_text_container);
	el_link_text = kite.browser.dom.ea('input', el_link_text_container);
	el_link_text.type = 'text';

	el_link_url_container = kite.browser.dom.ea('div', el_window);
	kite.browser.dom.ea('span', el_link_url_container).textContent = 'URL: ';
	el_url_message = kite.browser.dom.eac('span', el_link_url_container, 'message_failure');
	kite.browser.dom.ea('br', el_link_url_container);
	el_link_url = kite.browser.dom.ea('input', el_link_url_container);
	el_link_url.type = 'text';
	el_link_url.value = 'http://';

	el_buttons = kite.browser.dom.eac('div', el_window, 'wu-special_character_buttons');
	el_insert = kite.browser.dom.eac('button', el_buttons, 'button');
	el_insert.textContent = 'Insert link';
	el_cancel = kite.browser.dom.eac('button', el_buttons, 'button');
	el_cancel.textContent = 'Cancel';

	drop_down.set_content(el_window);

	el_window.addEventListener('click', function (e) {
		var value;

		if (el_insert === e.target) {
			if (el_link_text.value === '') {
				el_text_message.textContent = ' Please specify a link text';
			} else if (el_link_url.value === '') {
				el_url_message.textContent = ' Please specify a url';
			} else {
				value = {href : el_link_url.value};
				if (!insertion) {
					value.insertion = [{type : 'text', val : {text : el_link_text.value}, children : []}];
				}
				button.trigger(value);
				el_link_text.value = '';
				el_link_url.value = 'http://';
				drop_down.close();
			}
		} else if (el_cancel === e.target) {
			drop_down.close();
		}
	}, false);

	button.element = element;
	return button;
};


nbe.inputs.edit_link = function (trigger, title, parent, init) {
	var button, element, value, id, set_value, drop_down, el_window, el_link_url_container, el_link_url, el_buttons, el_insert, el_cancel;

	button = nbe.inputs.input('link', trigger);

	element = kite.browser.dom.eac('button', parent, 'wu-icon wu-icon-edit_link off');
	element.title = title;
	kite.browser.dom.ea('img', element).src = '/img/pen_alt2.svg';
	kite.browser.dom.ea('img', element).src = '/img/link.svg';

	value = null;
	id = null;

	set_value = function (new_value) {
		value = new_value;
		if (value) {
			id = value.id;
			el_link_url.value = value.href;
			element.className = 'wu-icon wu-icon-edit_link on';
		} else {
			el_link_url.value = '';
			element.className = 'wu-icon wu-icon-edit_link off';
		}
	};

	drop_down = new kite.browser.ui.Window();
	drop_down.set_title('Edit link');

	element.addEventListener('click', function (e) {
		e.stopPropagation();

		if (drop_down.is_open) {
			drop_down.close();
		} else {
			if (value) {
				drop_down.open();
			}
		}
	}, false);

	el_window = kite.browser.dom.ec('div', 'wu-special_characters');

	el_link_url_container = kite.browser.dom.ea('div', el_window);
	kite.browser.dom.ea('div', el_link_url_container).textContent = 'URL: ';
	el_link_url = kite.browser.dom.ea('input', el_link_url_container);
	el_link_url.type = 'text';

	el_buttons = kite.browser.dom.eac('div', el_window, 'wu-special_character_buttons');
	el_insert = kite.browser.dom.eac('button', el_buttons, 'button');
	el_insert.textContent = 'OK';
	el_cancel = kite.browser.dom.eac('button', el_buttons, 'button');
	el_cancel.textContent = 'Cancel';

	drop_down.set_content(el_window);

	el_window.addEventListener('click', function (e) {
		if (el_insert === e.target) {
			button.trigger({id : id, href : el_link_url.value});
			drop_down.close();
		} else if (el_cancel === e.target) {
			drop_down.close();
		}
	}, false);

	set_value(init);

	button.set_value = set_value;
	button.element = element;
	return button;
};


nbe.inputs.insert_image = function (trigger, title, parent) {
	var button, element, drop_down, el_window, el_src, el_width, el_height, el_title, el_buttons, el_insert, el_cancel;

	button = nbe.inputs.input('img', trigger);

	element = kite.browser.dom.eac('button', parent, 'wu-icon wu-icon-insert_image off');
	element.title = title;
	//element.textContent = '+ Image';

	drop_down = new kite.browser.ui.Window();
	drop_down.set_title('Insert image');

	element.addEventListener('click', function (e) {
		e.stopPropagation();

		if (drop_down.is_open) {
			drop_down.close();
		} else {
			drop_down.open();
		}
	}, false);

	el_window = kite.browser.dom.ec('div', 'wu-image_window');

	kite.browser.dom.ea('div', el_window).textContent = 'Image URL ';
	el_src = kite.browser.dom.ea('input', el_window);
	el_src.type = 'text';
	el_src.value = 'http://';

	kite.browser.dom.ea('div', el_window).textContent = 'Width ';
	el_width = kite.browser.dom.ea('input', el_window);
	el_width.type = 'text';

	kite.browser.dom.ea('div', el_window).textContent = 'Height ';
	el_height = kite.browser.dom.ea('input', el_window);
	el_height.type = 'text';

	kite.browser.dom.ea('div', el_window).textContent = 'Title ';
	el_title = kite.browser.dom.ea('input', el_window);
	el_title.type = 'text';

	el_buttons = kite.browser.dom.eac('div', el_window, 'wu-special_character_buttons');
	el_insert = kite.browser.dom.eac('button', el_buttons, 'button');
	el_insert.textContent = 'Insert image';
	el_cancel = kite.browser.dom.eac('button', el_buttons, 'button');
	el_cancel.textContent = 'Cancel';

	drop_down.set_content(el_window);

	el_window.addEventListener('click', function (e) {
		var value;

		if (el_insert === e.target) {
			value = {src : el_src.value};
			if (el_width.value !== '') {
				value.width = el_width.value;
			}
			if (el_height.value !== '') {
				value.height = el_height.value;
			}
			if (el_title.value !== '') {
				value.title = el_title.value;
			}
			button.trigger(value);
			el_src.value = 'http://';
			el_width.value = '';
			el_height.value = '';
			el_title.value = '';
			drop_down.close();
		} else if (el_cancel === e.target) {
			drop_down.close();
		}
	}, false);

	button.element = element;
	return button;
};


nbe.inputs.edit_image = function (trigger, title, parent, init) {
	var button, element, value, id, set_value, drop_down, el_window, el_src, el_width, el_height, el_title, el_buttons, el_insert, el_cancel;

	button = nbe.inputs.input('img', trigger);

	element = kite.browser.dom.eac('button', parent, 'wu-icon wu-icon-edit_image off');
	element.title = title;
	//element.textContent = 'Edit image';
	kite.browser.dom.ea('img', element).src = '/img/pen_alt2.svg';
	kite.browser.dom.ea('img', element).src = '/img/image.svg';

	value = null;
	id = null;

	set_value = function (new_value) {
		value = new_value;

		if (value) {
			id = value.id;
			el_src.value = value.src || '';
			el_width.value = value.width || '';
			el_height.value = value.height || '';
			el_title.value = value.title || '';
			element.className = 'wu-icon wu-icon-edit_image on';
		} else {
			el_src.value = '';
			el_width.value = '';
			el_height.value = '';
			el_title.value = '';
			element.className = 'wu-icon wu-icon-edit_image off';
		}
	};

	drop_down = new kite.browser.ui.Window();
	drop_down.set_title('Edit image');

	element.addEventListener('click', function (e) {
		e.stopPropagation();

		if (drop_down.is_open) {
			drop_down.close();
		} else {
			if (value) {
				drop_down.open();
			}
		}
	}, false);

	el_window = kite.browser.dom.ec('div', 'wu-image_window');

	kite.browser.dom.ea('div', el_window).textContent = 'Image URL ';
	el_src = kite.browser.dom.ea('input', el_window);
	el_src.type = 'text';
	el_src.value = 'http://';

	kite.browser.dom.ea('div', el_window).textContent = 'Width ';
	el_width = kite.browser.dom.ea('input', el_window);
	el_width.type = 'text';

	kite.browser.dom.ea('div', el_window).textContent = 'Height ';
	el_height = kite.browser.dom.ea('input', el_window);
	el_height.type = 'text';

	kite.browser.dom.ea('div', el_window).textContent = 'Title ';
	el_title = kite.browser.dom.ea('input', el_window);
	el_title.type = 'text';

	el_buttons = kite.browser.dom.eac('div', el_window, 'wu-special_character_buttons');
	el_insert = kite.browser.dom.eac('button', el_buttons, 'button');
	el_insert.textContent = 'OK';
	el_cancel = kite.browser.dom.eac('button', el_buttons, 'button');
	el_cancel.textContent = 'Cancel';

	drop_down.set_content(el_window);

	el_window.addEventListener('click', function (e) {
		var value;

		if (el_insert === e.target) {
			value = {id : id, src : el_src.value};

			if (el_width.value !== '') {
				value.width = el_width.value;
			}
			if (el_height.value !== '') {
				value.height = el_height.value;
			}
			if (el_title.value !== '') {
				value.title = el_title.value;
			}

			button.trigger(value);
			drop_down.close();
		} else if (el_cancel === e.target) {
			drop_down.close();
		}
	}, false);

	set_value(init);

	button.element = element;
	button.set_value = set_value;
	return button;
};


nbe.title.create = function (editor_id, options, doc) {
	var value, init, el_editor, set_value, detect_input, add_external_ops, get_value;

	init = function (state) {
		set_value(state.value);
	};

	if (options.editable) {

		el_editor = kite.browser.dom.ec('input', 'wu-title');
		el_editor.setAttribute('type', 'text');

		set_value = function (new_value) {
			value = new_value;

			if (el_editor.value !== value) {
				el_editor.value = value;
			}
			if (options.html_title) {
				document.title = value;
			}
		};

		detect_input = function (_event) {
			var new_value, op;

			new_value = el_editor.value;
			if (new_value !== value) {
				set_value(new_value);
				op = {editor_class : 'title', before : value, after : new_value};
				doc.add_ops(editor_id, [op]);
			}
		};

		el_editor.addEventListener('input', detect_input, false);
	} else {

		el_editor = document.createElement('div');

		set_value = function (new_value) {
			value = new_value;

			el_editor.textContent = value;
			if (options.html_title) {
				document.title = value;
			}
		};
	}

	add_external_ops = function (ops, _set_location) {
		ops.forEach(function (op) {
			if ('editor_class' in op && op.editor_class === 'title') {
				set_value(op.after);
			}
		});
	};

	get_value = function () {
		return value;
	};

	return {id : editor_id, el_editor : el_editor, init : init, add_external_ops : add_external_ops, get_value : get_value};
};


nbe.title.state_copy = function (state) {
	return {value : state.value};
};


nbe.title.state_init = function () {
	return {value : 'My Title'};
};


nbe.title.state_update = function (state, ops) {
	if (ops.length > 0) {
		state.value = ops[ops.length - 1].after;
	}
};


nbe.publish.create = function (editor_id, doc) {
	var time, init, msg, publish, add_external_ops, set_time, get_time;
 
	time = null;

	init = function (state) {
		set_time(state.time);
	};

	msg = document.createElement('div');

	publish = function (callback) {
		var html, body;
		
		html = nbe.doc.html(nbe.dynamic.doc);
			
		body = {
			type : 'publish',
			id : doc.ids.id,
			write : doc.ids.write,
			html : html
		};
			
		nbe.lib.xhr('POST', nbe.config.publish_url, {}, JSON.stringify(body), 0, function (response) {
			var op;
			
			response = JSON.parse(response);
			if (response === 'published') {
				op = {
					editor_class : 'publish',
					before : time,
					after : Date.now()
				};
				set_time(op.after);
				doc.add_ops(editor_id, [op]);
				callback(response);
			}
		}, function () {}, function () {
			callback(null);
		});
	};

	add_external_ops = function (ops, _set_location) {
		ops.forEach(function (op) {
			if ('editor_class' in op && op.editor_class === 'publish') {
				set_time(op.after);
			}
		});
	};

	set_time = function (new_time) {
		time = new_time;
		msg.textContent = time === null ? 'Not published' : 'Published at ' + new Date(time);
	};

	get_time = function () {
		return time;
	};

	return {id : editor_id, init : init, msg : msg, publish : publish, add_external_ops : add_external_ops, get_time : get_time};
};


nbe.publish.state_copy = function (state) {
	return {time: state.time};
};


nbe.publish.state_init = function () {
	return {time : null};
};


nbe.publish.state_update = function (state, ops) {
	if (ops.length > 0) {
		state.time = ops[ops.length - 1].after; 
	}
};


nbe.css.publish = '/* Line styles */\n\n.wu-line, .wu-line > span {\n	line-height : 160%;\n}\n\n.wu-line.wu-right {\n	text-align : right;\n}\n\n.wu-line.wu-center {\n	text-align : center;\n}\n\n.wu-line.wu-justify {\n	text-align : justify;\n}\n\n/* Line spacing */\n\n.wu-line_spacing_05, .wu-line_spacing_05 > span {\n	line-height : 50%;\n}\n\n.wu-line_spacing_06, .wu-line_spacing_06 > span {\n	line-height : 60%;\n}\n\n.wu-line_spacing_07, .wu-line_spacing_07 > span {\n	line-height : 70%;\n}\n\n.wu-line_spacing_08, .wu-line_spacing_08 > span {\n	line-height : 80%;\n}\n\n.wu-line_spacing_09, .wu-line_spacing_09 > span {\n	line-height : 90%;\n}\n\n.wu-line_spacing_10, .wu-line_spacing_10 > span {\n	line-height : 100%;\n}\n\n.wu-line_spacing_11, .wu-line_spacing_11 > span {\n	line-height : 110%;\n}\n\n.wu-line_spacing_12, .wu-line_spacing_12 > span {\n	line-height : 120%;\n}\n\n.wu-line_spacing_13, .wu-line_spacing_13 > span {\n	line-height : 130%;\n}\n\n.wu-line_spacing_14, .wu-line_spacing_14 > span {\n	line-height : 140%;\n}\n\n.wu-line_spacing_15, .wu-line_spacing_15 > span {\n	line-height : 150%;\n}\n\n.wu-line_spacing_16, .wu-line_spacing_16 > span {\n	line-height : 160%;\n}\n\n.wu-line_spacing_17, .wu-line_spacing_17 > span {\n	line-height : 170%;\n}\n\n.wu-line_spacing_18, .wu-line_spacing_18 > span {\n	line-height : 180%;\n}\n\n.wu-line_spacing_19, .wu-line_spacing_19 > span {\n	line-height : 190%;\n}\n\n.wu-line_spacing_20, .wu-line_spacing_20 > span {\n	line-height : 200%;\n}\n\n/* Lists */\n\n.wu-disc, .wu-square {\n	display : list-item;\n	list-style : inside;\n}\n\n.wu-lower-alpha, .wu-lower-roman , .wu-lower-roman, .wu-upper-alpha, .wu-upper-roman {\n	display : block;\n}\n\n.wu-disc {\n	list-style-type : disc;\n}\n\n.wu-lower-alpha:before {\n	counter-increment : item;\n	content : counter(item, lower-alpha) ". "\n}\n\n.wu-lower-roman:before {\n	counter-increment : item;\n	content : counter(item, lower-roman) ". "\n}\n\n.wu-square {\n	list-style-type : square;\n}\n\n.wu-upper-alpha:before {\n	counter-increment : item;\n	content : counter(item, upper-alpha) ". "\n}\n\n.wu-upper-roman:before {\n	counter-increment : item;\n	content : counter(item, upper-roman) ". "\n}\n\n.wu-ordered {\n	display : block;\n}\n\n.wu-ordered:before {\n	counter-increment : item;\n	content : counter(item) ". "\n}\n\n.wu-reset-counter {\n	counter-reset : item;\n}\n\n/* Heading */\n\n.wu-line.wu-heading1, .wu-line.wu-heading1 span {\n	display: block;\n	padding-top: 4px;\n	padding-bottom: 4px;\n	font-size: 135%;\n}\n\n.wu-line.wu-heading2, .wu-line.wu-heading2 span {\n	display: block;\n	padding-top: 4px;\n	padding-bottom: 4px;\n	font-size: 130%;\n}\n\n.wu-line.wu-heading3, .wu-line.wu-heading3 span {\n	display: block;\n	padding-top: 4px;\n	padding-bottom: 4px;\n	font-size: 125%;\n}\n\n.wu-line.wu-heading4, .wu-line.wu-heading4 span {\n	display: block;\n	padding-top: 4px;\n	padding-bottom: 4px;\n	font-size: 120%;\n}\n\n.wu-line.wu-heading5, .wu-line.wu-heading5 span {\n	display: block;\n	padding-top: 4px;\n	padding-bottom: 4px;\n	font-size: 115%;\n}\n\n.wu-line.wu-heading6, .wu-line.wu-heading6 span {\n	display: block;\n	padding-top: 4px;\n	padding-bottom: 4px;\n	font-size: 110%;\n}\n\n.wu-line.wu-heading1 span, .wu-line.wu-heading2 span, .wu-line.wu-heading3 span, .wu-line.wu-heading4 span, .wu-line.wu-heading5 span, .wu-line.wu-heading6 span {\n	display : inline-block;\n}\n\n/* Text styles */\n\n.wu-text.wu-bold {\n	font-weight : bold;\n}\n\n.wu-text.wu-underline {\n	text-decoration : underline;\n}\n\n.wu-text.wu-italic {\n	font-style : italic;\n}\n\n.wu-text.wu-strikethrough {\n	text-decoration : line-through;\n}\nbody {\n	margin : 0;\n}\n\ndiv.editor {\n	white-space : pre-wrap;\n	word-wrap : break-word;\n	font-size : 16px;\n	font-family : Arial;\n	line-height : 120%;\n	line-height : 160%;\n	padding : 30px 50px;\n}\n\ndiv.editor span {\n	font-size : 16px;\n	font-family : Arial;\n}\n';